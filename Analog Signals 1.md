# Signal-Processing
College project to plot signals ,its variation and the FT of it .
Fs = 10000;
t=-10:1/Fs:10;
m=2*(sinc(200*t)).^2 +(sinc(400*t)).^2;
figure;
plot (t,m);                                  
xlabel('Time(Seconds)');
ylabel('m(t)');
ylim([-0.1 3.5]);
xlim([-0.009 0.009]);
L = length(t);
figure;
n = length(m); 
y = fft(m);                           
f = (0:n-1)*(Fs/n);                         % frequency range
y = fftshift(y);                            % shift y values
f = (-n/2:n/2-1)*(Fs/n);                    % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlabel('Frequency')
ylabel('Transform')
ylim([-1*10^-4 6.5*10^-4]);
xlim([-1000 1000]);
grid on;

figure;
t=-2:1/Fs:2;                              %Changing Time period
m=2*(sinc(200*t)).^2 +(sinc(400*t)).^2;
n = length(m); 
y = fft(m);                           
f = (0:n-1)*(Fs/n);                         % frequency range
y = fftshift(y);                            % shift y values
f = (-n/2:n/2-1)*(Fs/n);                    % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlabel('Frequency')
ylabel('Transform')
ylim([-1*10^-4 35*10^-4]);
xlim([-1000 1000]);
grid on;

figure;
t=-10:3/Fs:10;                              %Changing Time step
m=2*(sinc(200*t)).^2 +(sinc(400*t)).^2;
n = length(m); 
y = fft(m);                           
f = (0:n-1)*(Fs/n);                         % frequency range
y = fftshift(y);                            % shift y values
f = (-n/2:n/2-1)*(Fs/n);                    % 0-centered frequency range
P = abs(y)/n;
plot (f,P);
xlabel('Frequency')
ylabel('Transform')
ylim([-1*10^-4 6.5*10^-4]);
xlim([-2000 2000]);
grid on;
