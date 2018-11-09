# CUDA-notes
cuda notes
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




