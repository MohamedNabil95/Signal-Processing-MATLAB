# Signal-Processing
College project to plot signals ,its variation and the FT of it .
clc
clear all
close all
fs  = 500000; % sampling frequency (fs > 2*BW)
Ts  = 1/fs; % sampling period
t   = -0.01:Ts:0.01-Ts ; % sampled time vector
global N ;
N = length(t); % calculate the number of samples
f   = -fs/2:fs/N:fs/2-fs/N; % frequency vector

m_t = 2*sinc(200*t).^2 + sinc(400*t).^2; % the message m(t)
c_t = cos(2*pi*20000*t); % the carrier c(t)
s_t = m_t.*c_t; %modulated signal s(t) = m(t) x c(t)
m_hilbert = imag(hilbert(m_t)); % the hilbert transform of the message m(t)
s_USB_t = (m_t.*cos(2*pi*20000*t) - m_hilbert.*sin(2*pi*20000*t)); % modulated signal s(t) = m(t) x c(t)
S_USB_f = fourier_transform(s_USB_t); % the spectrum of the modulated signal s(t)
S_USB_coherent = fourier_transform(s_USB_t.*c_t); % the spectrum of the modulated signal s(t) after Coherent Detection
U = lpf(f); % the low pass filter spectrum
X_f = S_USB_coherent .* U; % the modulated signal s(t) after Coherent Detection and filtering (the message)
x_t = inverse_fourier_transform(X_f); % the time domain representation of the signal after detection
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Upper Side Band of the modulated signal s(t) in Frequency domain
figure ('name','upper side band of the modulated signal ','NumberTitle','off','units','normalized','outerposition',[0 0 1 1]);
    plot(f/1000,abs(S_USB_f),'LineWidth',1)
    grid on;
    legend('S_U_S_B(f)')
   	title('Upper Side Band of the modulated signal s(t) in Frequency domain')
    xlabel('Frequency (kHz)'), ylabel('S_U_S_B(f)')
    xlim([-25 25])
    %print('upper side band of the modulated signal', '-dpng', '-r300'); %<-Save as PNG with 300 DPI
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% The Output of the coherent detector in Frequency domain (after multiplication)
figure ('name','The Output of the coherent detector (after multiplication) in Frequency domain','NumberTitle','off','units','normalized','outerposition',[0 0 1 1]);
 	hold on;
    plot(f/1000,abs(S_USB_coherent),'LineWidth',1)
    grid on;
    title('The Output of the coherent detector in Frequency domain (after multiplication)')
	legend('Low Pass Filter','Output of the coherent detector')
   	xlabel('Frequency (kHz)'), ylabel('S_U_S_B(f) x c(t)')
    xlim([-50 50])
    hold off;
    %print('The Output of the coherent detector in Frequency domain (after multiplication) ', '-dpng', '-r300'); %<-Save as PNG with 300 DPI
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% The Output of the coherent detector in Frequency domain (with LPF filter response)
figure ('name','The Output of the coherent detector in Frequency domain (with LPF filter response)','NumberTitle','off','units','normalized','outerposition',[0 0 1 1]);
 	hold on;
    plot(f/1000,U,'LineWidth',1)
    plot(f/1000,abs(S_USB_coherent),'LineWidth',1)
    grid on;
    title('The Output of the coherent detector in Frequency domain (with LPF filter response)')
	legend('Low Pass Filter','Output of the coherent detector')
   	xlabel('Frequency (kHz)'), ylabel('S_U_S_B(f) x c(t)')
    xlim([-50 50])
    hold off;
    %print('The Output of the coherent detector in Frequency domain (with LPF filter response)', '-dpng', '-r300'); %<-Save as PNG with 300 DPI
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% The Output of the coherent detector in Time domain (after filtering)
figure ('name','The Output of the coherent detector in Time domain (after filtering)','NumberTitle','off','units','normalized','outerposition',[0 0 1 1]);
    hold on;
    plot(t*1000,abs(x_t),'LineWidth',1)
    plot(t*1000,m_t,'LineWidth',1)
    grid on;
    title('The Output of the coherent detector in Time domain (after filtering)')
	legend('the message after demodulation','the orignal message')
   	xlabel('Time (msec)'), ylabel('m(t)')
    hold off;
    %print('The Output of the coherent detector in Time domain (after filtering)', '-dpng', '-r300'); %<-Save as PNG with 300 DPI
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% The Output of the coherent detector in Frequwncy domain (after filtering)
figure ('name','The Output of the coherent detector after filter in Frequwncy domain ','NumberTitle','off','units','normalized','outerposition',[0 0 1 1]);
    plot(f/1000,abs(X_f),'LineWidth',1)
    grid on;
    legend('Coherent Detector Output')
   	title('The Output of the coherent detector in Frequency domain (after filtering)')
    xlabel('Frequency (kHz)'), ylabel('Coherent Detector Output')
    xlim([-1 1])
    %print('The Output of the coherent detector in Frequwncy domain after filter', '-dpng', '-r300'); %<-Save as PNG with 300 DPI
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function X_f = fourier_transform(x_t)

	global N
  	X_f = (1/N)*(fftshift(fft(x_t))); % computes DTFS i.e. the frequency representation of x(t)
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function x_t = inverse_fourier_transform(X_f)
	global N
  	x_t = N*ifft(ifftshift(X_f)); % computes Inverse of DTFS i.e. the time domain representation of x(t)
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%s
function u = lpf(f)
    N=length(f);
    u=zeros(1,N);
    for k=1:N
        if (f(k) >= -500 && f(k) <= 500)
            u(k) = 1;
        else
            u(k) = 0;
        end
    end
end
