# Représentation temporelle et fréquentielle d'un signal

  • 1 • On va tracer le signal x(t), Dans les deux domaines, temporelle et fréquentille ;
      dans le domaine fréquentielle avec une fréquence d'échantillonnage fe = 10000Hz et un nombre d'échantillons N = 5000 :

  ```
  |  clear all 
  |  close all 
  |  clc
  |  
  |  fe = 1e4 ;    % Fréquence d'échantillonnage du signal
  |  te  = 1/fe;   ‰ Le pas 
  |  N = 10000;    ‰ Le nombre d'échantillons 
  |  
  |  t = (0:N-1)*te;
  |  fshift = (-N/2:N/2-1)*(fe/N);
  |  
  |  x = 1.2*cos(2*pi*440*t + 0.2) + 1*cos(2*pi*550*t)+ 0.6*cos(2*pi*2500*t);
  |  plot(t,x,'.')
  ```
  
  • 2 - 3 • On calcule la TFD du signal x(t) , puis on trace son spectre :
  
  ```
  |  % On utilise la commande fft pour calculer la TFD du signal pour qu'on puisse le tracer dans le domaine fréquenciel
  |  y = fft(x);
  |
  |  % Grace à abs, on peut afficher le spectre d'amplitude
  |  % fftshift pour centrer le résultat sur le zero
  |  plot(fshift,fftshift(2*abs(y)/N));
  ```
  
  • 4 - 5 - 6 - 7 • Création d'un bruit xnoise - bruit blanc gaussien ; 
  
  ```
  |  % Grace à la commande rand , on a pu générer un bruit aléatoire
  |  % On multiplie x2 pour augmenter l'intensité du bruit généré
  |  xnoise = 2*randn(size(x));
  |
  |  ‰ On Affiche le spectre du bruit 
  |  plot(fshift,fftshift(abs(xnoise)));
  |
  |  % On écoute ce bruit généré grce à la commande sound
  |  sound(noise);
  ```
  
  # Analyse fréquentielle du chant du rorqual bleu
  
  • 1 - 2 • On télecharge le fichier "bluewhale.au" et on écoute son contenu en utilisant la commande audioread puis sound :
  
  ```
  |  [x,fs] = audioread("bluewhale.au");
  |  sound(w,fs);
  |  plot(x);
  ```

  • 3 • On spécifie une nouvelle longuer pour le signal :

  ```
  |  sound(w,2*fs);
  |  plot(x);
  ```
