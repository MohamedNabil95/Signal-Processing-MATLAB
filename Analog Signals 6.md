# Signal-Processing
College project to plot signals ,its variation and the FT of it .
Fs=1000000;   Ts=1/Fs;
w = 2*pi*4000; 
t = 0:1/Fs:4*(1/4000)-Ts; 
Th=2*pi*rand(1000,1); %theta vector with 1000 value from 0 to 2pi
n=length(t);

plot(Th);

grid on; 
xlabel('t (sec.)');
figure;
for k=1:4,  %plotting 4 random samples 
    subplot(2,2,k)
    
    x=cos(w*t+Th(k));
    plot(t,x), hold all;
    title(' random samples')
    grid on; 
    xlabel('t (sec.)');
    
end
%par 3 and 4
 x=@(t,Th)cos(w*t+Th);
Avg=integral(@(Th) x(0,Th), 0,2*pi); %average Ensemble (part 3 )
figure;
plot(t,Avg);
xlabel('t (sec.)');
hold on
Avg_time=mean(cos((w*t)+Th(1))); %time Average (part 4 );
plot(t,Avg_time);
title('Average Ensemble And Average time')
hold off

%Result of averages are Values with "10^-17" which is really small 
%but because Matlab is solving numerical there is an error and we can
%consider Result of averages is Zero

%part 5 
figure;
tau=t;
Coe_rela=0.5*cos(w*tau);       %auto coerelation
 plot (tau,Coe_rela
