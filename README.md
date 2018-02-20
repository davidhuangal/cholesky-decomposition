# cholesky-decomposition
Simple octave program to compute the Cholesky factor of an n-by-n symmetric, positive-definite matrix.

## Usage
Obtain the n-by-n symmetric, positive-definite matrix that you want to compute the Cholesky factor of.
Let's say you define it as the matrix A.
Run the program as follows:

```octave
cholesky(A, n)
```
where A is your matrix and n is its order.

What will be returned is the upper-triangular Cholesky factor.

## Example Use
```octave

% Creating a random 5x5 matrix, A
M = rand(5);
A = M'*M

A =

   1.41147   0.50368   0.72197   0.90387   0.65699
   0.50368   0.23568   0.32488   0.27783   0.30763
   0.72197   0.32488   0.78400   0.50235   0.83792
   0.90387   0.27783   0.50235   1.14882   0.53843
   0.65699   0.30763   0.83792   0.53843   0.96092
   
% Set the Cholesky factor to a matrix called R
R = cholesky(A, 5)

R =

   1.18805   0.42395   0.60769   0.76080   0.55300
   0.00000   0.23652   0.28434  -0.18905   0.30942
   0.00000   0.00000   0.57781   0.16230   0.71630
   0.00000   0.00000   0.00000   0.71269   0.08412
   0.00000   0.00000   0.00000   0.00000   0.19803
   
```
