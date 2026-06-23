<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>MATLAB Experiments</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background: #f4f6f8;
      color: #1f2937;
    }

    .container {
      max-width: 900px;
      margin: 0 auto;
    }

    h1 {
      margin: 0 0 16px;
      font-size: 28px;
    }

    .note {
      margin: 0 0 20px;
      color: #6b7280;
    }

    .card {
      background: #ffffff;
      border: 1px solid #d1d5db;
      border-radius: 12px;
      padding: 16px;
      margin-bottom: 16px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.04);
    }

    .card-head {
      display: flex;
      gap: 12px;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      margin-bottom: 12px;
    }

    .card h2 {
      margin: 0;
      font-size: 20px;
    }

    .btn {
      border: 0;
      background: #2563eb;
      color: #fff;
      padding: 10px 14px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
    }

    pre {
      margin: 0;
      padding: 14px;
      background: #0f172a;
      color: #e2e8f0;
      border-radius: 10px;
      overflow: auto;
      white-space: pre-wrap;
      word-break: break-word;
      font-size: 14px;
      line-height: 1.6;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="card">
      <div class="card-head">
        <h2>Experiment 1</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp2main">EXPERIMENT 1
Write a MATLAB program to generate two sinusoidal signals using the equation:
y(t) = sin(2πft)
where the frequencies are f₁ = 2 Hz and f₂ = 10 Hz. Consider the time range from t = 0 to t = 1 seconds with a step size of 0.01. Perform the following operations and plot the results using the subplot command:
Plot both sinusoidal signals
Addition of the two signals
Subtraction of the two signals
Multiplication of the two signals
Label the axes as time and amplitude, and give suitable titles for each plot.

PROGRAM:
clc; clear all; close all;
t=0:0.01:1
y1=sin(2*pi*2*t)
y2=sin(2*pi*10*t)
a=y1+y2;
s=y1-y2;
m=y1.*y2;
subplot(2,2,1);
plot(t,y1,t,y2);
xlabel('time -->');
ylabel('amplitude -->');
title('sinosoidal signal');
subplot(2,2,2);
plot(t,a);
xlabel('time -->');
ylabel('amplitude -->');
title('addition');
subplot(2,2,3);
plot(t,s);
xlabel('time -->');
ylabel('amplitude -->');
title('subtraction');
subplot(2,2,4);
plot(t,m);
xlabel('time -->');
ylabel('amplitude -->');
title('multiplication');</pre>
    </div>
    <div class="card">
      <div class="card-head">
        <h2>Experiment 2</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp2">EXPERIMENT 2
Write a MATLAB program to generate two sinusoidal signals using the equation:
y(t) = sin(2πft)
where the frequencies are f₁ = 2 Hz and f₂ = 10 Hz. Consider the time range from t = 0 to t = 1 seconds with a step size of 0.01.
Perform the following operations using separate user-defined function files:
Addition of the two signals
Subtraction of the two signals
Multiplication of the two signals
Write a main MATLAB program to call these functions and plot the original signals and the resulting signals using the subplot command with proper axis labels and titles.
PROGRAM:
clc; clear all; close all;
t=0:0.01:1;
y1=sin(2*pi*2*t);
y2=sin(2*pi*10*t);
subplot (2,2,1);
plot(t,y1,t,y2);
xlabel('time -->');
ylabel('amplitude -->');
title('sinosoidal signal');
subplot(2,2,2);
plot(t,a);
xlabel('time -->');
ylabel('amplitude -->');
title('addition');
subplot(2,2,3);
plot(t,s);
xlabel('time -->');
ylabel('amplitude -->');
title('subtraction');
subplot(2,2,4);
plot(t,m);
xlabel('time -->');
ylabel('amplitude -->');
title('multiplication');
function [a,s,m] = process(y1,y2)
a=y1+y2;
s=y1-y2;
m=y1.*y2;
end</pre>
    </div>


    <div class="card">
      <div class="card-head">
        <h2>Experiment 3</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp3">EXPERIMENT 3
Write a MATLAB program to generate a set of 50 data points using the linear model:
y = −0.3x + 0.2r
where r is a normally distributed random number. Consider x = 1, 2, 3, …, 50. Use MATLAB commands to determine the best linear fit using polynomial curve fitting.
PROGRAM:
clc;clear all;close all;
x=1:50;
y=-0.3*x+0.2*randn(1,50);
p=polyfit(x,y,1);
f=polyval(p,x)
plot(x,y,'o',x,f,'-')
legend('data','linear fit')
xlabel('X values --->');
ylabel('Y values --->');
title('Linear Curve Fitting');</pre>
    </div>

    <div class="card">
      <div class="card-head">
        <h2>Experiment 4</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp4">EXPERIMENT 4
Write a MATLAB program to generate 10 equally spaced points in the interval 0 to 4r. Compute the sine values of these points and obtain a third-degree polynomial approximation using polynomial curve fitting.Evaluate the fitted polynomial over the interval O to 4r and plot the original data points and the approximated curve.

PROGRAM:
clc; clear all; close all;
x = linspace(0,4*pi,10);
y = sin(x);
p = polyfit(x,y,3);
x1 = linspace(0,4*pi);
f = polyval(p,x1);
plot(x,y,'o',x1,f,'-')
legend('data points','cubic fit')
xlabel('X values --->');
ylabel('Y values --->');
title('Polynomial Curve Fitting')</pre>
    </div>

    <div class="card">
      <div class="card-head">
        <h2>Experiment 5</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp5">EXPERIMENT 5
Write a MATLAB program to evaluate the definite integral:
I=|^pai÷2(down 0) x sin(x),dx

using Simpson’s  rule with  subintervals. Display the computed value of the integral.
PROGRAM:
clc;clear all;close all;
f=@(x)x*sin(x)
a=0;
b=pi/2;
n=20;
h=(b-a)/n;
s=f(a)+f(b);
for i=1:2:n-1
s=s+4*f(a+i*h)
end
for i=2:2:n-2
s=s+2*f(a+i*h); 
end
I=(h/3)*s;
display(I)</pre>
    </div>

    <div class="card">
      <div class="card-head">
        <h2>Experiment 6</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp6">EXPERIMENT 6
Write a MATLAB program to numerically evaluate the definite integral
|^5^0(x²+2x+1)dx
using the Trapezoidal Rule with 10 equal subintervals.

PROGRAM:
clc;clear all;close all;
f = @(x) x^2 + 2*x + 1; 
a = 0; 
b = 5; 
n = 10; 
h = (b - a)/n;
sum = f(a) + f(b);
for i = 1:n-1
x = a + i*h;
sum = sum + 2*f(x);
end
I= (h/2) * sum;
fprintf ('Integral using Trapezoidal Rule, I = %.6f\n', I);</pre>
    </div>

    <div class="card">
      <div class="card-head">
        <h2>Experiment 7</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp7">EXPERIMENT 7
Write a MATLAB program to:
1. Find the eigenvalues and eigenvectors of a given matrix A
2. Find the inverse of the matrix
3. Verify that:
4. 
PROGRAM 
clc;
clear;
Close all;
A = input('Enter matrix A: ');
% Eigenvalues and Eigenvectors
[V, D] = eig(A);
disp('Eigenvalues (D):');
disp(D);
disp('Eigenvectors (V):');
disp(V);
% Inverse of matrix
A_inv = inv(A);
disp('Inverse of matrix A:');
disp(A_inv);
% Verification
I = A * A_inv;
disp('Verification (A * A_inv):');
disp(I);</pre>
    </div>

    <div class="card">
      <div class="card-head">
        <h2>Experiment 8</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp8">EXPERIMENT 8
Solve the following system of linear algebraic equations using Gauss Elimination Method and obtain the solution vector using MATLAB:
6x +3y+2z=6
6x+4y+3z=0
20x+ 15y +12z=0

PROGRAM 
clc; clear;
A=[632; 643; 201512];
b= [6;0;0];Aug= [Ab];n = size(A, 1);
for i= 1:n-1
for j= i+1n
factor = Aug(j,i)/Aug(i, i);
Aug(,)= Aug(j,)- factor*Aug
end
end
x = Zeros(n, I);
for i=n:-1:1
sum_val = Aug(i,i+ 1:n)*x(i+1:n);
x(i)= (Aug(i, end) - sum_val)/Aug(i, );
end
disp('Solution is:")
disp(x)</pre>
    </div>

    <div class="card">
      <div class="card-head">
        <h2>Experiment 9</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp9">EXPERIMENT 9
Write a MATLAB program to find a root of the equation
f(2)=2x^2-5x+3= 0
using the Newton-Raphson method.
· Take the initial guess as co = 0
Use a tolerance of 10-7
Perform iterations until convergence or up to 100 iterations
Display the root and number of iterations

PROGRAM :
f=@(x)x-(2*×^2-5*×+3)/(4*×-5):
0=X
tol=1e-7:
for iteration=1:100
xnew=f(x):
if abs(xnew-x)>tol x=xnew;
else
break
end
end
fprintf(“Root=%f at iteration no.%d\n', xnew, iteration)</pre>
    </div>

    <div class="card">
      <div class="card-head">
        <h2>Experiment 10</h2>
        <button class="btn">Copy Code</button>
      </div>
      <pre id="exp10">EXPERIMENT 10
Wite a MATLAB program to compute the Discrete Fourier Transform (DFT) of the sequenc.
[n] = [1, 2, 3, 4) using the DFT formula

PROGRAM 
x=[1, 2, 3, 4];N=length(x);X=zeros(1, N);for k=0:N-1
for n=0:N-1
X(k+I)=X(k+1)+x(n+1)*exp(-li*2*pi*k*n/N);
end
end
display(X);</pre>
    </div>
  </div>

  <script>
    document.querySelectorAll('.card').forEach((card) => {
      const button = card.querySelector('button.btn');
      const codeBlock = card.querySelector('pre');

      if (!button || !codeBlock) {
        return;
      }

      button.addEventListener('click', async () => {
        const originalText = button.textContent;

        try {
          await navigator.clipboard.writeText(codeBlock.innerText.trim());
          button.textContent = 'Copied';
        } catch (error) {
          button.textContent = 'Copy failed';
        }

        setTimeout(() => {
          button.textContent = originalText;
        }, 1000);
      });
    });
  </script>
</body>
</html>
