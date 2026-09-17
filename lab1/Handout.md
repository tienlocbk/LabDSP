disp('Ex1.1 - 1')
x = 1:4
y = x + 1

disp('Ex1.1 - 2')
x = 1:4
y = 5:8
z = x .* y

disp('Ex1.1 - 3')
x = linspace(0, %pi, 10)
y = sin(x)

disp('Ex1.2 - 1')
T = 0.1;
t = 0:0.0001:T;
xa = 3*sin(100*%pi*t);
plot(t, xa)

disp('Ex1.2 - 2')
Tn = linspace(0, T, 30);
x = 3*sin(100*%pi*Tn);
plot(Tn, x)

disp('Ex1.2 - 3')
delta = 0.1;
xq = delta * floor(x/delta);
plot2d3(Tn, xq);

disp('Ex1.2 - single window')
clf();
subplot(3,1,1); plot(t, xa); xtitle('xa(t) - 5 periods', 't (s)', 'Amplitude');
subplot(3,1,2); plot2d3(Tn, x); xtitle('x(n) - sampled, Fs=300', 'n', 'Amplitude');
subplot(3,1,3); plot2d3(Tn, xq); xtitle('xq(n) - quantized, delta=0.1', 'n', 'Amplitude');
