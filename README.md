# cholesky-decomposition
Simple octave program to compute the Cholesky factor of a positive definite, symmetric matrix.


```matlab
function [R] = cholesky(A, n)
  
  for i=1:n
    if (A(i, i) <= 0)
      disp("The matrix is not positive definite.");
      return;
    endif
  endfor
  
  R = zeros(n);
  
  for i=1:n
    for j=1:n
      if(i == j)
        squares = 0;
        for k=1:j-1
          squares = squares + (R(j,k))^2;
        endfor
        R(j,j) = sqrt(A(j,j) - squares);      
      elseif(i > j)
        summation = 0;
        for k=1:j-1
          summation = summation+ R(i,k)*R(j,k);
        endfor
        R(i,j) = ((A(i,j)-summation)/(R(j,j)));
      endif
    endfor
  endfor
  
  R = R';
  
endfunction
```
