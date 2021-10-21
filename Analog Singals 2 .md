# Signal-Processing
College project to plot signals ,its variation and the FT of it .
%PART 2
%DSB-LC
fsm=1000000;
tsm=1/fsm;
tm=-0.006:tsm:0.006;
m5=2*(sinc(1000*tm)).^3;
c=cos(2*pi*20000*tm);
ka1=1/3;
ka2=0.5;
ka3=1;
ka4=10;
ka5=50;
s1=(1+(ka1*m5)).*c;
s2=(1+(ka2*m5)).*c;
s3=(1+(ka3*m5)).*c;
s4=(1+(ka4*m5)).*c;
s5=(1+(ka5*m5)).*c;

[envelop_s1,lo] = envelope(s1);
[envelop_s2,lo] = envelope(s2);
[envelop_s3,lo] = envelope(s3);
[envelop_s4,lo] = envelope(s4);
[envelop_s5,lo] = envelope(s5);

figure(1);
subplot(2,1,1)
plot(tm,s1);
title('DSB-LC modulated signal with modulation index ka1=1/3');
xlabel('t');
ylabel('s1(t)');
subplot(2,1,2)
plot(tm,envelop_s1);
title('DSB-LC envelope modulated signal with modulation index ka1=1/3');
xlabel('t');
ylabel('s1(t)');

figure(2);
subplot(2,1,1)
plot(tm,s2);
title('DSB-LC modulated signal with modulation index ka1=0.5');
xlabel('t');
ylabel('s2(t)');
subplot(2,1,2)
plot(tm,envelop_s2);
title('DSB-LC envelope modulated signal with modulation index ka1=0.5');
xlabel('t');
ylabel('s2(t)');

figure(3);
subplot(2,1,1)
plot(tm,s3);
title('DSB-LC modulated signal with modulation index ka1=1');
xlabel('t');
ylabel('s3(t)');
subplot(2,1,2)
plot(tm,envelop_s3);
title('DSB-LC envelope modulated signal with modulation index ka1=1');
xlabel('t');
ylabel('s3(t)');

figure(4);
subplot(2,1,1)
plot(tm,s4);
title('DSB-LC modulated signal with modulation index ka1=10');
xlabel('t');
ylabel('s4(t)');
subplot(2,1,2)
plot(tm,envelop_s4);
title('DSB-LC envelope modulated signal with modulation index ka1=10');
xlabel('t');
ylabel('s4(t)');

figure(5);
subplot(2,1,1)
plot(tm,s5);
title('DSB-LC modulated signal with modulation index ka1=50');
xlabel('t');
ylabel('s5(t)');
subplot(2,1,2)
plot(tm,envelop_s5);
title('DSB-LC envelope modulated signal with modulation index ka1=50');
xlabel('t');
ylabel('s5(t)');
figure;
n = length(m5);
y = fft(m5);
f = (-n:n-1)*(fsm/n); % frequency range
y = fftshift(y); % shift y values
f = (-n/2:n/2-1)*(fsm/n); % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlabel('Frequency')
ylabel('Transform')
grid on;

figure(7);
n = length(s1);
y = fft(s1);
f = (0:n-1)*(fsm/n); % frequency range
y = fftshift(y); % shift y values
f = (-n/2:n/2-1)*(fsm/n); % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlabel('Frequency')
ylabel('Transform')
grid on;

 figure(8) ;
spectrogram(s1,'yaxis') ;
title('Spectrogram of Modulated DSB LC ') ;

%DSB-SC

m5=2*(sinc(1000*tm)).^3;
c=cos(2*pi*20000*tm);

s=(m5).*c;


[envelop_s1,lo] = envelope(s);

figure(9);
plot(tm,s);
title('DSB-SC modulated signal');
xlabel('t');
ylabel('s(t)');


figure(10);
plot(tm,envelop_s1);
title('DSB-SC envelope modulated signal ');
xlabel('t');
ylabel('s(t)');


figure(11);
n = length(s);
y = fft(s);
f = (0:n-1)*(fsm/n); % frequency range
y = fftshift(y); % shift y values
f = (-n/2:n/2-1)*(fsm/n); % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlabel('Frequency')
ylabel('Transform')
grid on;

 figure(12) ;
spectrogram(s,'yaxis') ;
title('Spectrogram of Modulated DSB SC ') ;
