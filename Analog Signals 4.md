# Signal-Processing
College project to plot signals ,its variation and the FT of it .
Fs=10000000;
Ts=1/Fs;
KF= 30000;
t=[-0.001:Ts:0.001];
m=2*(sinc(1000*t)).^3;
Fi = 40000*2*pi+(KF*2*pi*m);
s=cos(cumtrapz(t,Fi));


figure(1);

yyaxis left
plot(t,s);
ylabel('FM Modulated Signal')
yyaxis right
plot(t,Fi);
ylabel('Fi of Modulated Signal')

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

kf=[100 1000 10000 100000];

figure(2);
for i=1:4
    
        Fi2 = 40000*2*pi+(kf(i)*m);
        s2=cos(cumtrapz(t,Fi2));
        subplot(2,2,i)
        yyaxis left
        plot(t,s2); 
        ylabel('S(t))
        yyaxis right
        plot(t,Fi2);
                ylabel('instantous frequency')
        title(['Sfm(t)at Kf= ' num2str(kf(i)) '.'])
        xlabel('t(Sec)')
        xlim([-0.001 0.001]);
        grid on ;

end

   
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
figure(3)
spectrogram(s,256,120,256,Fs,'yaxis')
title('Spectrogram of FM Modulated signal ') ;
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
figure(4)

m1=2*(sinc(1000*t)).^3;
Fi1 = 40000*2*pi+(150*2*pi*m1);
s1=cos(cumtrapz(t,Fi1));

spectrogram(s1,256,120,256,Fs,'yaxis')
title('Spectrogram of FM Modulated signal at Kf=150 Hz/V') ;
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
figure(5)
n = length(s);
y = fft(s);
f = (0:n-1)*(Fs/n); % frequency range
y = fftshift(y); % shift y values
f = (-n/2:n/2-1)*(Fs/n); % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlim([0 1.5e5]);
xlabel('Frequency')
ylabel('s(f)')
grid on;
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
figure(6)
n = length(m);
y = fft(m);
f = (0:n-1)*(Fs/n); % frequency range
y = fftshift(y); % shift y values
f = (-n/2:n/2-1)*(Fs/n); % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlim([0 1.5e5]);
xlabel('Frequency')
ylabel('M(f)')
grid on;
%%%%%%%%%%%%%%%%%
figure(7)
obw(y,1000000)
%%%%%%%%%%%%%%%%
uuuu=max(KF*m);
