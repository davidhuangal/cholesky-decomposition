# Cholesky Factorization
### David Huangal
Simple octave program to compute the Cholesky factor of an n-by-n symmetric,
positive-definite matrix

## Code
```matlab
function [R] = cholesky(A)

  assert(issymmetric(A) == 1, "Not symmetric.")
  % Create the empty R matrix
  [n, nn] = size(A);
  R = zeros(n);

  % Fill the R matrix
  for i=1:n
    for j=1:n
      if(i == j)
        squares = 0;
        for k=1:j-1
          squares = squares + (R(j,k))^2;
        endfor
        temp = A(j,j) - squares;
        % Check for positive definite.
        assert(temp > 0, "Not positive definite.");
        R(j,j) = sqrt(temp);
      elseif(i > j)
        summation = 0;
        for k=1:j-1
          summation = summation+ R(i,k)*R(j,k);
        endfor
        R(i,j) = ((A(i,j)-summation)/(R(j,j)));
      endif
    endfor
  endfor

  % We actually want the upper triangular version of R
  % So just redifine R as its transpose
  R = R';

  % Check that R is upper triangular
  assert(istriu(R) == 1, "R is not upper triangular.");


endfunction


```

## Usage
```matlab
cholesky(A)
```
Where A is the matrix you would like to compute the Cholesky factorization of. This program returns the Cholesky factor of A.

## Example Use
### Successful Case
```matlab
% Creating a random 5x5 symmetric matrix, A
M = rand(5);
A = M'*M

A =

   1.14933   1.20441   1.20958   0.84202   1.72476
   1.20441   1.73185   1.16849   0.86968   1.78777
   1.20958   1.16849   1.50215   1.03254   1.93960
   0.84202   0.86968   1.03254   0.86421   1.35647
   1.72476   1.78777   1.93960   1.35647   2.71516

% Compute the Cholesky factor and set it to the variable R
R = cholesky(A)

R =

   1.07207   1.12344   1.12827   0.78541   1.60882
   0.00000   0.68537  -0.14453  -0.01850  -0.02867
   0.00000   0.00000   0.45636   0.31491   0.26355
   0.00000   0.00000   0.00000   0.38448   0.02436
   0.00000   0.00000   0.00000   0.00000   0.23662

% To show that A = R'*R, subtract them to see if the resulting matrix
% is very close to all zeros.

test = A-R'*R

test =

   2.2204e-16   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00
   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00
   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00
   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00
   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00   0.0000e+00

```

### Failed Case 1: A is not symmetric

```matlab
A = rand(5,5)

A =

   0.995013   0.206674   0.512598   0.034540   0.804127
   0.699311   0.249647   0.761727   0.895891   0.450996
   0.618100   0.982516   0.167178   0.067177   0.648571
   0.656604   0.306086   0.290738   0.444524   0.715611
   0.418638   0.963720   0.079895   0.544143   0.884931

R = cholesky(A)

error: Not symmetric.
error: called from
    assert at line 94 column 11
    cholesky at line 3 column 3

```

### Failed Case 2: A is not positive definite
```matlab
A = [0 4 5; 4 4 6; 5 6 3]

A =

   0   4   5
   4   4   6
   5   6   3

% Clearly the matrix is symmetric.
% However, it is not positive definite.

R = cholesky(A)

error: Not positive definite.
error: called from
    assert at line 94 column 11
    cholesky at line 17 column 9

```
