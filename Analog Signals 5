# Signal-Processing
College project to plot signals ,its variation and the FT of it .
% 5.1

fs=10000000;
t= -0.01:1/fs:0.01;
m = 2*(sinc(1000*t)).^3; % fm=1500 Hz
fc=40000; %(Hz)
kp=10; 
C = cos(fc*2*pi*t); %carrier 
s=cos(fc*2*pi*t+kp*m); % modulated signal 
g=gradient(m,t);
dev=(kp/(2*pi))*g; %  inst frequency deviation in (Hz)
fi=(fc+dev); %inst frequency

figure(1); % plotting s(t) and deviation
subplot(2,1,1)
plot(t,s);
title('modulated signal wave form')
xlabel('t(Sec)')
ylabel('s(t)(V)')
xlim([-0.01 0.01])
grid on;
hold on 
subplot(2,1,2)
plot(t,dev);
title('instantaneous frequency Deviation ')
xlabel('t(Sec)')
ylabel('deltaf(t)')
xlim([-0.01 0.01])
grid on;
hold off

figure(2); %plotting s(t) and deviation on each other
plot(t,s);
title('modulated signal wave form')
xlabel('t(Sec)')
ylabel('s(t)(V)')
xlim([-0.01 0.01])
grid on;
hold on 
plot(t,dev*1e-5,'r');
title('instantaneous frequency Deviation ')
xlabel('t(Sec)')
ylabel('deltaf(t)')
xlim([-0.01 0.01])
grid on;
hold off
%%
figure(3)   % calculate M(f)
M = fft(m);
n = length(M);
M_shift=fftshift(M)/n;
f_pm =(-n/2:n/2-1)*(fs/n);
plot(f_pm,abs(M_shift));
title(['M(f) Vs frequency '],'FontSize', 18);
xlabel('Frequency(Hz)','fontweight','bold','FontSize', 16);
ylabel('M(f)','fontweight','bold','FontSize', 16);
xlim([-15000 15000]);
grid();
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% 5.2 
kp=[1 10 100 1000];

figure(4); % Different kp
for i=1:4
    
        s =cos((fc*2*pi*t)+(kp(i)*m));
        subplot(2,2,i)
        plot(t,s);
        title(['Spm(t)at Kp= ' num2str(kp(i)) '.'])
        xlabel('t(Sec)')
        ylabel('Spm(t)(V)')
        xlim([-0.001 0.001]);
        grid on ;

end

% 5.3

figure(5); % spectrogram kp=10
kp=10;
s=cos((fc*2*pi*t)+(kp*m));
spectrogram(s,[],[],[],fs,'yaxis');
title('spectrogram of Spm(t) at Kp=10');
% 5.4

figure(6);  % spectrogram kp=100
kp=100;
s=cos((fc*2*pi*t)+(kp*m));
spectrogram(s,[],[],[],fs,'yaxis');
title('spectrogram of Spm(t) at Kp=100');

% 5.5

kp=10;
m = 2*(sinc(1000*t)).^3;
maximum_dev=max(dev); % delta f

%% S(f) frequency domain

S = fft(s);
n = length(S);
S_shift=fftshift(S)/n;
f_pm =(-n/2:n/2-1)*(fs/n);

figure(7)
plot(f_pm,abs(S_shift));
title(['S(f) Vs frequency '],'FontSize', 18);
xlabel('Frequency(Hz)','fontweight','bold','FontSize', 16);
ylabel('S(f)','fontweight','bold','FontSize', 16);
xlim([-100000 100000]);
grid();
