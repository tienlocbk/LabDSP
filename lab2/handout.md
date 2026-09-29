disp('exercise 4')
n = -5:5;
msignal = bool2s(n >= 0);
ur = n.*msignal
clf();
plot2d3(n, ur);
title('ur(n) - unit ramp'); xlabel('n'); ylabel('Amplitude');

//exercise 5 
disp('exercise 5')
n = -1:1;
x = [1, 3, -2];

xr = x($:-1:1);       
xe = 0.5*(x + xr);    
xo = 0.5*(x - xr);   

clf();
subplot(3,1,1)
plot2d3(n, x);
title('x(n)'); xlabel('n'); ylabel('Amplitude');

subplot(3,1,2);
plot2d3(n, xe);
title('xe(n)'); xlabel('n'); ylabel('Amplitude');

subplot(3,1,3);
plot2d3(n, xo);
title('xo(n)'); xlabel('n'); ylabel('Amplitude');

//Exercise 6
disp('Exercise 6')
n1 = 0:3;
x1 = [0, 1, 3, -2];

n2 = -1:2;
x2 = [0, 1, 2, 3];

n_start = min(n1(1), n2(1));
n_end   = max(n1($), n2($));
n = n_start:n_end;

x1e = zeros(1, length(n));
x2e = zeros(1, length(n));
x1e(n1 - n_start + 1) = x1;
x2e(n2 - n_start + 1) = x2;

y = x1e + x2e;

clf();
subplot(3,1,1); plot2d3(n, x1e); title('x1(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,1,2); plot2d3(n, x2e); title('x2(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,1,3); plot2d3(n, y);   title('y(n) = x1(n)+x2(n)'); xlabel('n'); ylabel('Amplitude');


// Exercise 7
disp('Exercise 7')
n1 = 0:3;
x1 = [0, 1, 3, -2];

n2 = -1:2;
x2 = [0, 1, 2, 3];

n_start = min(n1(1), n2(1));
n_end   = max(n1($), n2($));
n = n_start:n_end;

x1e = zeros(1, length(n));
x2e = zeros(1, length(n));
x1e(n1 - n_start + 1) = x1;
x2e(n2 - n_start + 1) = x2;

y = x1e .* x2e;  

clf();
subplot(3,1,1); plot2d3(n, x1e); title('x1(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,1,2); plot2d3(n, x2e); title('x2(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,1,3); plot2d3(n, y);   title('y(n) = x1(n).x2(n)'); xlabel('n'); ylabel('Amplitude');
