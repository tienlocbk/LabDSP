// Exercise 1 - Delay
disp('Exercise 1')
function [yn, yorigin] = delay(xn, xorigin, k)
    yn = xn;
    yorigin = xorigin - k;
    // Position xorigin is n = 0.
    nx = (1:length(xn)) - xorigin;
    ny = (1:length(yn)) - yorigin;
    clf();
    subplot(2,1,1); plot2d3(nx, xn);
    title('x(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(2,1,2); plot2d3(ny, yn);
    title('y(n) = x(n-k)'); xlabel('n'); ylabel('Amplitude');
endfunction

[yn, yorigin] = delay([1, -2, 3, 6], 3, 1);
disp(yn, 'yn ='); disp(yorigin, 'yorigin =');

// Exercise 2 - Advance
disp('Exercise 2')
function [yn, yorigin] = advance(xn, xorigin, k)
    yn = xn;
    yorigin = xorigin + k;
    // Position xorigin is n = 0.
    nx = (1:length(xn)) - xorigin;
    ny = (1:length(yn)) - yorigin;
    clf();
    subplot(2,1,1); plot2d3(nx, xn);
    title('x(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(2,1,2); plot2d3(ny, yn);
    title('y(n) = x(n+k)'); xlabel('n'); ylabel('Amplitude');
endfunction

[yn, yorigin] = advance([1, -2, 3, 6], 3, 1);
disp(yn, 'yn ='); disp(yorigin, 'yorigin =');

// Exercise 3 - Fold
disp('Exercise 3')
function [yn, yorigin] = fold(xn, xorigin)
    yn = xn($:-1:1);
    yorigin = length(xn) - xorigin + 1;
    // Position xorigin is n = 0.
    nx = (1:length(xn)) - xorigin;
    ny = (1:length(yn)) - yorigin;
    clf();
    subplot(2,1,1); plot2d3(nx, xn);
    title('x(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(2,1,2); plot2d3(ny, yn);
    title('y(n) = x(-n)'); xlabel('n'); ylabel('Amplitude');
endfunction

[yn, yorigin] = fold([1, -2, 3, 6], 3);
disp(yn, 'yn ='); disp(yorigin, 'yorigin =');

// Exercise 4 - Addition
disp('Exercise 4')
function [yn, yorigin] = add(x1n, x1origin, x2n, x2origin)
    n1 = (1:length(x1n)) - x1origin;
    n2 = (1:length(x2n)) - x2origin;
    n_start = min(n1(1), n2(1));
    n_end = max(n1($), n2($));
    n = n_start:n_end;
    // Put both signals on the same n axis; other samples are zero.
    x1e = zeros(1, length(n));
    x2e = zeros(1, length(n));
    x1e(n1 - n_start + 1) = x1n;
    x2e(n2 - n_start + 1) = x2n;
    yn = x1e + x2e;
    yorigin = 1 - n_start;
    clf();
    subplot(3,1,1); plot2d3(n, x1e);
    title('x1(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(3,1,2); plot2d3(n, x2e);
    title('x2(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(3,1,3); plot2d3(n, yn);
    title('y(n) = x1(n) + x2(n)'); xlabel('n'); ylabel('Amplitude');
endfunction

[yn, yorigin] = add([0, 1, 3, -2], 1, [1, 1, 2, 3], 2);
disp(yn, 'yn ='); disp(yorigin, 'yorigin =');

// Exercise 5 - Multiplication
disp('Exercise 5')
function [yn, yorigin] = multi(x1n, x1origin, x2n, x2origin)
    n1 = (1:length(x1n)) - x1origin;
    n2 = (1:length(x2n)) - x2origin;
    n_start = min(n1(1), n2(1));
    n_end = max(n1($), n2($));
    n = n_start:n_end;
    // Put both signals on the same n axis; other samples are zero.
    x1e = zeros(1, length(n));
    x2e = zeros(1, length(n));
    x1e(n1 - n_start + 1) = x1n;
    x2e(n2 - n_start + 1) = x2n;
    yn = x1e .* x2e;
    yorigin = 1 - n_start;
    clf();
    subplot(3,1,1); plot2d3(n, x1e);
    title('x1(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(3,1,2); plot2d3(n, x2e);
    title('x2(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(3,1,3); plot2d3(n, yn);
    title('y(n) = x1(n) . x2(n)'); xlabel('n'); ylabel('Amplitude');
endfunction

[yn, yorigin] = multi([0, 1, 3, -2], 1, [1, 1, 2, 3], 2);
disp(yn, 'yn ='); disp(yorigin, 'yorigin =');

// Exercise 6 - Convolution
disp('Exercise 6')
function [yn, yorigin] = convolution(xn, xorigin, hn, horigin)
    yn = zeros(1, length(xn) + length(hn) - 1);
    // Each pair xn(i)*hn(j) contributes to output position i+j-1.
    // The two for loops visit every pair of input samples.
    for i = 1:length(xn)
        for j = 1:length(hn)
            yn(i+j-1) = yn(i+j-1) + xn(i)*hn(j);
        end
    end
    yorigin = xorigin + horigin - 1;
    // Position xorigin is n = 0.
    nx = (1:length(xn)) - xorigin;
    nh = (1:length(hn)) - horigin;
    ny = (1:length(yn)) - yorigin;
    clf();
    subplot(3,1,1); plot2d3(nx, xn);
    title('x(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(3,1,2); plot2d3(nh, hn);
    title('h(n)'); xlabel('n'); ylabel('Amplitude');
    subplot(3,1,3); plot2d3(ny, yn);
    title('y(n) = x(n) * h(n)'); xlabel('n'); ylabel('Amplitude');
endfunction

[yn, yorigin] = convolution([1, -2, 3, 6], 3, [1, 2, 1], 2);
disp(yn, 'yn ='); disp(yorigin, 'yorigin =');

// Problem 2.1 - Shifting and folding
disp('Problem 2.1')
function y = signal21(n)
    y = (1+n/3).*bool2s(n >= -3 & n <= -1) ...
        + bool2s(n >= 0 & n <= 3);
endfunction
n = -8:8;
x = signal21(n);
xf = signal21(-n);
xd = signal21(n-4);
yb1 = signal21(4-n);     // Fold, then delay by 4.
yb2 = signal21(-n-4);    // Delay by 4, then fold.
yc = signal21(-n+4);
xdelta = (1/3)*bool2s(n == -2) + (2/3)*bool2s(n == -1);
xdelta = xdelta + bool2s(n == 0) + bool2s(n == 1) ...
    + bool2s(n == 2) + bool2s(n == 3);
xstep = (1+n/3).*(bool2s(n >= -3)-bool2s(n >= 0)) ...
        + bool2s(n >= 0)-bool2s(n >= 4);
disp(signal21(-3:3), 'x(n), n = -3:3:');
disp(xdelta, 'Impulse representation:');
disp(xstep, 'Step representation:');
clf();
subplot(3,2,1); plot2d3(n,x); title('(a) x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,2); plot2d3(n,xf); title('Intermediate: x(-n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,3); plot2d3(n,yb1); title('(b1) x(4-n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,4); plot2d3(n,xd); title('Intermediate: x(n-4)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,5); plot2d3(n,yb2); title('(b2) x(-n-4)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,6); plot2d3(n,yc); title('(c) x(-n+4)'); xlabel('n'); ylabel('Amplitude');

// Problem 2.2 - Signal transformations
disp('Problem 2.2')
function y = signal22(n)
    y = bool2s(n >= -1 & n <= 2) ...
        + 0.5*bool2s(n >= 3 & n <= 4);
endfunction
n = -6:8;
x = signal22(n);
ya = signal22(n-2);
yb = signal22(4-n);
yc = signal22(n+2);
yd = x.*bool2s(n <= 2);
ye = signal22(n-1).*bool2s(n == 3);
yf = signal22(n.^2);
xe = 0.5*(x+signal22(-n));
xo = 0.5*(x-signal22(-n));
disp([n; x; ya; yb; yc; yd; ye; yf; xe; xo], ...
     'Rows: n, x, (a), (b), (c), (d), (e), (f), (g), (h)');
clf();
subplot(3,2,1); plot2d3(n,x); title('x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,2); plot2d3(n,ya); title('(a) x(n-2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,3); plot2d3(n,yb); title('(b) x(4-n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,4); plot2d3(n,yc); title('(c) x(n+2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,5); plot2d3(n,yd); title('(d) x(n)u(2-n)'); xlabel('n'); ylabel('Amplitude');
clf();
subplot(3,2,1); plot2d3(n,x); title('x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,2); plot2d3(n,ye); title('(e) x(n-1)delta(n-3)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,3); plot2d3(n,yf); title('(f) x(n^2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,4); plot2d3(n,xe); title('(g) Even part'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,5); plot2d3(n,xo); title('(h) Odd part'); xlabel('n'); ylabel('Amplitude');

// Problem 2.4 - Even and odd decomposition
disp('Problem 2.4')
n = -2:2;
x = [2, 3, 4, 5, 6];
xr = x($:-1:1);
xe = 0.5*(x+xr);
xo = 0.5*(x-xr);
disp(xe, 'xe(n) ='); disp(xo, 'xo(n) =');
clf();
subplot(3,1,1); plot2d3(n, x);
title('x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,1,2); plot2d3(n, xe);
title('xe(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,1,3); plot2d3(n, xo);
title('xo(n)'); xlabel('n'); ylabel('Amplitude');

// Problem 2.6 - Time invariance
disp('Problem 2.6')
function y = pulse26(n)
    y = bool2s(n >= 0 & n <= 3);
endfunction
n = -4:8;
x = pulse26(n);
x2 = pulse26(n-2);

// (a), (b): T[x(n)] = x(n^2).
y = pulse26(n.^2);
ydelay = pulse26((n-2).^2);
y2 = pulse26(n.^2-2);
clf();
subplot(3,2,1); plot2d3(n,x); title('(1) x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,2); plot2d3(n,y); title('(2) y(n) = x(n^2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,3); plot2d3(n,ydelay); title('(3) y(n-2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,4); plot2d3(n,x2); title('(4) x2(n) = x(n-2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,5); plot2d3(n,y2); title('(5) T[x2(n)]'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,6); plot2d3(n,y2-ydelay); title('(6) T[x2(n)] - y(n-2)'); xlabel('n'); ylabel('Amplitude');

disp(y2-ydelay, 'Difference for (b):');

// (c): T[x(n)] = x(n)-x(n-1).
y = pulse26(n)-pulse26(n-1);
ydelay = pulse26(n-2)-pulse26(n-3);
y2 = pulse26(n-2)-pulse26(n-3);
clf();
subplot(3,2,1); plot2d3(n,x); title('(1) x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,2); plot2d3(n,y); title('(2) y(n) = x(n)-x(n-1)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,3); plot2d3(n,ydelay); title('(3) y(n-2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,4); plot2d3(n,x2); title('(4) x2(n) = x(n-2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,5); plot2d3(n,y2); title('(5) T[x2(n)]'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,6); plot2d3(n,y2-ydelay); title('(6) T[x2(n)] - y(n-2)'); xlabel('n'); ylabel('Amplitude');

disp(y2-ydelay, 'Difference for (c):');

// (d): T[x(n)] = n*x(n).
y = n.*pulse26(n);
ydelay = (n-2).*pulse26(n-2);
y2 = n.*pulse26(n-2);
clf();
subplot(3,2,1); plot2d3(n,x); title('(1) x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,2); plot2d3(n,y); title('(2) y(n) = n*x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,3); plot2d3(n,ydelay); title('(3) y(n-2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,4); plot2d3(n,x2); title('(4) x2(n) = x(n-2)'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,5); plot2d3(n,y2); title('(5) T[x2(n)]'); xlabel('n'); ylabel('Amplitude');
subplot(3,2,6); plot2d3(n,y2-ydelay); title('(6) T[x2(n)] - y(n-2)'); xlabel('n'); ylabel('Amplitude');
disp(y2-ydelay, 'Difference for (d):');
