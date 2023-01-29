# 1 • Définition du signal

```
clear all
close all
clc

Te = 5*1e-4;

f1 = 500;
f2 = 400;
f3 = 50;
t = 0:Te:5-Te;
fe = 1/Te;
N = length(t);

fshift = (-N/2:N/2-1)*(fe/N);
f = (0:N-1)*(fe/N);

x = sin(2*pi*f1*t)+sin(2*f2*pi*t)+sin(2*pi*f3*t);
```

# 2 • On trace le signal et sa TFD

```
y = fft(x);

figure(1);
subplot(2,1,1)
plot(t,x)

subplot(2,1,2)
plot(fshift, fftshift(abs(y)));
```

# 3 • Transmitance complexe

• 1 • Tracé du module de H(f)

```
k = 1;
wc = 50;

h = (k*1j*((2*pi*f)/wc))./(1+1j*((2*pi*f)/wc));

figure(2);
semilogx(abs(h))
plot(abs(h))
legend("Module de h(f)")
```

• 2 • On trace 20.log(|H(f)|) pour différentes pulsations de coupure wc

```
wc2 = 500;
wc3 = 1000;

h1 = (k*1j*((2*pi*f)/wc2))./(1+1j*((2*pi*f)/wc2));
h2 = (k*1j*((2*pi*f)/wc3))./(1+1j*((2*pi*f)/wc3));

G = 20*log(abs(h));
G1 = 20*log(abs(h1));
G2 = 20*log(abs(h2));

P = angle(h);
P1 = angle(h1);
P2 = angle(h2);

figure(3);
subplot(3,1,1)
semilogx(f,G,f,G1,f,G2);
title("Diagramme de Bode")
xlabel("rad/s")
ylabel("decibel")
legend("G : wc=50","G1 : wc=500","G2 : wc=1000")

subplot(3,1,2)
semilogx(f,P,f,P1,f,P2)
legend("G : wc=50","G1 : wc=500","G2 : wc=1000")
````

-> On observe qu'à mesure que la fréquence de coupure augmente, la transmittance du filtre augmente également, 
   ce qui signifie que le filtre est de plus en plus "ouvert" pour les fréquences élevées.
   

# Filtre réel

```
% filtre en utilisant la fonction butter
wc2 = 500;
wc3 = 900;
[b1, a1] = butter(1, wc/(fe/2),'high'); 
[b2, a2] = butter(1, wc2/(fe/2),'high');
[b3, a3] = butter(1, wc3/(fe/2),'high');

% Application du filtre au signal
y1 = filter(b1, a1, x);
y2 = filter(b2, a2, x);
y3 = filter(b3, a3, x);

% tranformée de Fourier du signal filtré
y1_fourier = fft(y1);
y2_fourier = fft(y2);
y3_fourier = fft(y3);

% tracés des signaux filtrés et leurs transformées de Fourier
figure(4);
subplot(3,2,1);
plot(t, y1);
title('Signal filtré avec wc = 50');
subplot(3,2,2);
plot(t, y1);
plot(abs(y1_fourier))
title('y1_Fourier');

subplot(3,2,3);
plot(t, y2);
title('Signal filtré avec wc = 400');
subplot(3,2,4);
plot(abs(y2_fourier))
title('y2_Fourier');

subplot(3,2,5);
plot(t, y3);
title('Signal filtré avec wc = 500');
subplot(3,2,6);
plot(abs(y3_fourier))
title('y3_Fourier');
```

-> En choisissant différentes fréquences de coupure et en les utilisant pour 
   filtrer le signal dans l'espace des fréquences, on peut constater que plus
   la fréquence de coupure est élevée, plus les fréquences plus élevées du signal 
   sont amplifiées, tandis que les fréquences inférieures sont atténuées.
   
# On choisi le filtre

-> wc = 500 ;    Car à cette fréquence, il n'altère pas les informations qu'on souhaite
                 garder et reduit considérablement celles qu'on souhaite supprimer(wc=50)
                 
# On compare le resultat

```
figure(5)
plot(t,x,'g')
xlim([0 4*1e-2])
hold on
plot(t,y2)
xlim([0 4*1e-2])
legend("Signal non filtré","Signal filtré")
```

-> C'est proche du résultat qu'on cherche 
   
