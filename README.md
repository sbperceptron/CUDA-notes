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
!["Add_vectors"](https://github.com/sbperceptron/CUDA-notes/blob/master/add.c)

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

!["Add_ Matrices"](https://github.com/sbperceptron/CUDA-notes/blob/master/addmat.c)

there is a limit to the number of threads per block, since all threads of a block 
are expected to reside on the same processor core and must share the limited memory
resources of that core. on current gpus a thread block may contain up to 1024 threads.

however, a kernel can be executed by multiple equally shaped thread blocks, so thaat 
the total number of threads is equal to the number of threads per block times the number of 
blocks.

blocks are organized into a one dimensional, two dimensional or three dimensional 
grid of thread blocks

!["Thread Blocks"](https://github.com/sbperceptron/CUDA-notes/blob/master/grid-of-thread-blocks.png)

each block within the grid can be identified by a one dimensional , two dimensioanl or 
three dimensional index accessible within the kernek through the built-in blockIdx
variable. the dimesnion of the thred block is accessible within the kernel through the builtin
blockDim variable.

 

Given the heterogeneous nature of the cuda programming model, a typical sequence 
of operations for a cuda c program is
1. Declare and allocate host and device memory. 
2. initialize host data.
3. transfer data from the host to device
4. excecute one or more kernels.
5. transfer results from the device to the host.

saxpy single precision a*x plus y 
it is a good hello world example for parallel computaion

