# Représentation temporelle et fréquentielle d'un signal

• 1 • On va tracer le signal x(t), Dans les deux domaines, temporelle et fréquentille ;
      dans le domaine fréquentielle avec une fréquence d'échantillonnage fe = 10000Hz et un nombre d'échantillons N = 5000.
      
      ’’’
  |  clear all 
  |  close all 
  |  clc
  |  
  |  fe = 1e4 ; 
  |  te  = 1/fe; 
  |  N = 10000;
  |  
  |  t = (0:N-1)*te;
  |  fshift = (-N/2:N/2-1)*(fe/N);
  |  
  |  x = 1.2*cos(2*pi*440*t + 0.2) + 1*cos(2*pi*550*t)+ 0.6*cos(2*pi*2500*t);
  |  %plot(t,x,'.')
  |  
  |  y = fft(x);
  |  %plot(fshift,fftshift(2*abs(y)/N));
      ’’’
