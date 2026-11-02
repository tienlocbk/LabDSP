# Lab 4 — Scilab exercises 4–7

Exercises 1–3 are derived in the report.

```scilab
// Exercise 4 - Audio data using built-in Scilab functions
// Run this file from SciNotes, or execute one exercise block at a time.
disp('Exercise 4');
output_dir = get_absolute_file_path('lab4.sce') + 'output/';
Fs = 8000;
t = (0:Fs-1)/Fs;
audio = 0.6*sin(2*%pi*440*t);
wavwrite(audio, Fs, 16, output_dir + 'tone.wav');
[recorded, sample_rate, bits] = wavread(output_dir + 'tone.wav');
quiet = 0.5*recorded;
wavwrite(quiet, sample_rate, 16, output_dir + 'quiet_tone.wav');
disp(sample_rate, 'Sampling rate (Hz) =');
disp(bits, 'Bits per sample =');
disp(length(recorded), 'Number of samples =');
// Optional playback: playsnd(quiet, sample_rate);
clf();
subplot(2,1,1); plot(t(1:160), recorded(1:160));
title('Original 440 Hz tone'); xlabel('Time (s)'); ylabel('Amplitude');
subplot(2,1,2); plot(t(1:160), quiet(1:160));
title('Gain = 0.5'); xlabel('Time (s)'); ylabel('Amplitude');

// Exercise 5 - Grayscale image, histogram and 3 by 3 mean blur
// IPCV is an image-processing toolbox; this demo uses basic matrices.
disp('Exercise 5');
I = 40*ones(64,64);
I(17:48,17:48) = 180;
I(25:40,25:40) = 240;
counts = zeros(1,256);
for row = 1:64
    for col = 1:64
        level = I(row,col);
        counts(level+1) = counts(level+1) + 1;
    end
end
// Keep the outer border unchanged; average each interior 3 by 3 block.
B = I;
for row = 2:63
    for col = 2:63
        B(row,col) = sum(I(row-1:row+1,col-1:col+1))/9;
    end
end
disp([counts(41), counts(181), counts(241)], 'Counts at 40, 180, 240 =');
clf();
gcf().color_map = graycolormap(256);
subplot(2,2,1); Matplot(I+1);
title('Original grayscale image');
subplot(2,2,2); Matplot(round(B)+1);
title('3 by 3 mean blur');
subplot(2,2,3); plot2d3(0:255, counts);
title('Original histogram'); xlabel('Gray level'); ylabel('Pixel count');
subplot(2,2,4); plot(1:64, [I(32,:); B(32,:)]');
title('Row 32: original and blurred'); xlabel('Column'); ylabel('Gray level');
legend('Original', 'Blurred');

// Exercise 6 - Linear convolution: folding/shifting and matrix methods
disp('Exercise 6');
x = [1, 2, -3, 2, 1];
h = [1, 0, -1];
L = length(x) + length(h) - 1;
y_fold = zeros(1,L);
// At output n, x(n-k) is x folded about k=0 and shifted right by n.
// Outside the stored x interval the sample is zero.
for n = 0:L-1
    for k = 0:length(h)-1
        j = n-k;
        if j >= 0 & j < length(x) then
            y_fold(n+1) = y_fold(n+1) + h(k+1)*x(j+1);
        end
    end
end
// Column j+1 is h shifted right by j, with zero padding.
H = zeros(L,length(x));
for j = 0:length(x)-1
    H(j+1:j+length(h),j+1) = h';
end
y_matrix = (H*x')';
Ex = sum(abs(x).^2);
Ey = sum(abs(y_fold).^2);
disp(H, 'Convolution matrix H =');
disp(y_fold, 'Folding and shifting result =');
disp(y_matrix, 'Matrix result =');
disp([Ex, Ey], 'Total energies [Ex, Ey] =');
clf();
subplot(2,2,1); plot2d3(0:length(x)-1, x);
title('x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(2,2,2); plot2d3(0:L-1, y_fold);
title('Linear convolution y(n)'); xlabel('n'); ylabel('Amplitude');
subplot(2,2,3); plot2d3(0:length(x)-1, abs(x).^2);
title('Input energy per sample, Ex = 19'); xlabel('n'); ylabel('|x(n)|^2');
subplot(2,2,4); plot2d3(0:L-1, abs(y_fold).^2);
title('Output energy per sample, Ey = 42'); xlabel('n'); ylabel('|y(n)|^2');

// Exercise 7 - Circular convolution: folding/shifting and matrix methods
disp('Exercise 7');
x = [1, 2, -3, 2, 1];
h = [1, 0, -1, -1, 1];
N = length(x);
y_fold = zeros(1,N);
// Adding N keeps the remainder argument nonnegative in this example.
for n = 0:N-1
    for k = 0:length(h)-1
        j = modulo(n-k+N,N);
        y_fold(n+1) = y_fold(n+1) + h(k+1)*x(j+1);
    end
end
// A circulant matrix: column j+1 is h circularly delayed by j.
C = zeros(N,N);
for n = 0:N-1
    for j = 0:N-1
        C(n+1,j+1) = h(modulo(n-j+N,N)+1);
    end
end
y_matrix = (C*x')';
Ex_period = sum(abs(x).^2);
Ey_period = sum(abs(y_fold).^2);
disp(C, 'Circulant matrix C =');
disp(y_fold, 'Folding and shifting result =');
disp(y_matrix, 'Matrix result =');
disp([Ex_period, Ey_period], 'Energies per period [Ex, Ey] =');
disp([Ex_period/N, Ey_period/N], 'Average powers [Px, Py] =');
clf();
subplot(2,2,1); plot2d3(0:N-1, x);
title('One period of x(n)'); xlabel('n'); ylabel('Amplitude');
subplot(2,2,2); plot2d3(0:N-1, y_fold);
title('One period of circular y(n)'); xlabel('n'); ylabel('Amplitude');
subplot(2,2,3); plot2d3(0:N-1, abs(x).^2);
title('Input energy per sample, period sum = 19'); xlabel('n'); ylabel('|x(n)|^2');
subplot(2,2,4); plot2d3(0:N-1, abs(y_fold).^2);
title('Output energy per sample, period sum = 50'); xlabel('n'); ylabel('|y(n)|^2');
```
