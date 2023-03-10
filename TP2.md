# Jeux de mots

 • 1 - 2 • Apres avoir Sauvegarder le fichier sur le répertoire de travail, puis l'avoir dans MATLAB à l’aide de la commande « audioread »,
      On trace le signal le signal enregistré et on l'ecoute en utilisant la commande sound :
      
  ```
  |   % On sauvegarde le fichier audio sur votre répertoire de travail et puis
  |   % on le charge en utilisant la commande audioread
  |   [x,fs] = audioread('phrase.wave');
  |   
  |   % On trace le signal dans le domaine temporel
  |   t = (0:length(x)-1)/fs; % Création d'un vecteur de temps
  |   plot(t,x); % Tracé du signal en fonction du temps
  |   xlabel('Temps (s)');
  |   ylabel('Amplitude');
  |   
  |   % On écoute le signal en utilisant la commande sound
  |   sound(x,fs);
  ```
  
  • 3 • On compresse et dilate le signal en changeant la fréquence 
  
   ```
  |   sound(x, 2*fs);       % Dilatation : son de Terminator
  |   sound(x, 0.5*fs);     % Compression : son de Donald Duck
  ```
  
  • 5 • On segmente la première partie de la phrase " rien ne sert de "
  
  ```
  |   % seg1 contient le valeurs de x (la phrase) contenant " rien ne sert de "
  |   riennesertde = x(1:130106);
  |   sound (riennesertde, fs);
  |   plot (riennesertde);
  ```
  
  • 6 • On crée les segments qui restent
  
  ```
  |   courir = x(130107:190006);
  |   sound (courir,fs);
  |   
  |   ilfaut = x(190007:250006);
  |   sound (ilfaut, fs);
  |   
  |   partirapoint = x (250007:394240);
  |   sound (partirapoint, fs);
 
  ```
  
  • 7 • On réarange les segments
  
  ```
  |   phrase = [riennesertde;partirapoint;ilfaut;courir];
  |   sound (phrase,fs);
  ```
  
  # Synthèse et analyse spectrale d’une gamme de musique
 
  ```
  |   clear all
  |   close all
  |   clc
  |   
  |   % Fréquence d'échantillonnage
  |   fe=8192;
  |   
  |   % Vecteur temps
  |   t=0:1/fe:1;
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "Do1"
  |.  % le nombre 262 par exemple dans ce cas represente la fréquence de la note Do1
  |   Do1=sin(2*pi*262*t);
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "Re"
  |   Re=sin(2*pi*294*t);
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "Mi"
  |   Mi=sin(2*pi*330*t);
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "Fa"
  |   Fa=sin(2*pi*t*349);
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "Sol"
  |   Sol=sin(2*pi*t*392);
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "La"
  |   La=sin(2*pi*t*440);
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "Si"
  |   Si=sin(2*pi*t*494);
  |   
  |   % Générer la forme d'onde sinusoidale pour la note "Do2"
  |   Do2=sin(2*pi*t*523);
  |   
  |   % Créer un tableau "G" qui contient les notes 
  |   G=[Do1 Re Mi Fa Sol La Si Do2];
  ```
