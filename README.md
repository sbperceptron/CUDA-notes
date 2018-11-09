# CUDA-notes
cuda notes
# Kernels
cuda c extends c by allowing the programmer to define c functions, called kernels, 
that, when called are excecuted n times in parallel by n different cuda kernels, 
as opposed to only once like regular c functions.

a kernel is defined using __global__ declaration specifier and the number of cuda 
threads that execute that kernel for a given kernel call is specified using a new
<<<...>>> excecution configuration syntax. each thread that ececutes the kernel is 
given a unique thread id that is accessible within the kernel through the built in 
threadIdx variable

the following code add two vectors a and b of size n and stores the result into a 
vector c
!["Add"](https://github.com/sbperceptron/CUDA-notes/blob/master/add.c)

here each of the N threads that excecute VecAdd() performs one pair wise addition

# Thread hierarchy 
For convenience threadIdx is a 3 component vector, so that threads can be identified using
a one dimensional, two dimensional or three dimensional thread index, forming a one 
dimensional, two dimensional or three dimensional blick of threads called thread blick
this provides a natural wat to invoke computation across the elements in a domain
such as a vector, matrix, or volume.

the index of a thread and its thread id relate to each other in astraight forward way
. For a one dimensional block, they are the same ; for a two dimensional block of 
size Dx, Dy the thread id of a thread of index x,y is x+yDx; for a three dimensional block og
size Dx, Dy , Dz the thread id of a thread of index x,y,z is x+yDx+zDxDy

for example the code below adds two matricesa A and B of size NXN and stores the 
result into matrix c





