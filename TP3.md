Dans ce TP on cherche a Supprimer le bruit autour du signal produit par un électrocardiographefaire et faire la représentation temporelle et
fréquentielle en utilisant la transformée de fourrier discrète TFD.

# Suppression du bruit provoqué par les mouvements du corps

  • 1 - 2 • On charge le fichier contenant le signal ECG en utilisant la commande load , et on le trace dans le domaine temporel :
  
  ```
  |   clear all
  |   close all 
  |   clc
  |   
  |   fe = 500 ; 
  |   te = 1/fe;
  |   N = 4170;
  |   t=0:te:(N-1)*te;
  |
  |   load('ecg.mat')
  |   
  |   subplot(2,2,1)
  |   plot(t,ecg);
  |   xlabel("Temps");
  |   ylabel("Amplitude");
  ```
  
  • 3 - 4 • On trace notre signal dans le domaine frequentiel pour visualiser les fréquences ,en utilisant la TFD :
  
  ```
  |   subplot(2,2,2)
  |   fshift = (-N/2:N/2-1)*(fe/N);
  |   spectre_ecg = fft(ecg);
  |   plot(fshift,fftshift(2*abs(spectre_ecg)/N));
  |   xlabel("frequence");
  |   ylabel("amplitude");
  ```
   -> On peut maintenant utiliser notre filtre ideal passe-haut pour éliminer les bruits dues aux mouvements du corps.
   -> On régle les fréquences inférieures à 50Hz à zero grace à notre filtre :
   
  ```
  |   subplot(2,2,3)
  |   pass_haut_ideal = ones(size(ecg));    % Notre filtre passe haut
  |   fc = 0.5;                             % La fréquence de coupure
  |   indexe_fc = ceil((fc*N)/fe);
  |   pass_haut_ideal(1:indexe_fc)=0;
  |   pass_haut_ideal(N-indexe_fc+1:N)=0;
  |   f=(0:N-1)*(fe/N);                    
  ```
   -> Et puis on obtient le résultat aprés filtrage du signal :
   
   ```
  |   ecg1 = pass_haut_ideal .* spectre_ecg;
  |   
  |   tmp_ecg_filre = ifft(ecg1,'symmetric');
  |   plot(t,tmp_ecg_filre);
  ```
  
  # Suppression des interférences des lignes électriques 50Hz

  • 5 - 6 • On utilise un filtre Notch pour supprimer la composante de 50Hz , et on visualise le résultat :
  
  ```
  |   pass_notch_ideal = ones(size(ecg));
  |   fc = 50; 
  |   indexe_fc = ceil((fc*N)/fe)+1;
  |   pass_notch_ideal(indexe_fc)=0;
  |   pass_notch_ideal(N-indexe_fc+1)=0;
  |   
  |   ecg2= pass_notch_ideal .* fft(tmp_ecg_filre);
  |   
  |   tmp_ecg2_filre = ifft(ecg2,'symmetric');
  |   subplot(311)
  |   plot(t,ecg);
  |   subplot(312)
  |   plot(t,tmp_ecg2_filre);
  |   subplot(313)
  |   plot(t,ecg-tmp_ecg2_filre);
  ```

  # Identification de la fréquence cardiaque avec la fonction d’autocorrélation
  
   -> La fréquence cardiaque peut être identifiée à partir de la fonction d'autocorrélation du signal ECG. Cela se fait en cherchant
   le premier maximum local après le maximum global (à tau = 0) de cette fonction.

   -> On utilise la fonction xcorr pour le signal ecg3
  
  ```
  |   pass_bas_ideal = zeros(size(ecg));
  |   fc3 = 20; 
  |   indexe_fc3 = ceil((fc3*N)/fe);
  |   pass_bas_ideal(1:indexe_fc3)=1;
  |   pass_bas_ideal(N-indexe_fc3+1:N)=1;
  |   
  |   ecg3 = pass_bas_ideal .* fft(tmp_ecg2_filre);
  |   
  |   tmp_ecg3_filre = ifft(ecg3,'symmetric');
  |
  |   subplot(311)
  |   plot(t,ecg);
  |
  |   subplot(312)
  |   plot(t,tmp_ecg2_filre);
  |
  |   subplot(313)
  |   plot(t,tmp_ecg3_filre);
  |
  |   [c,lags] = xcorr(tmp_ecg3_filre,tmp_ecg3_filre);
  |   stem(lags/fe,c)
  ```
  
   -> On detecte une correlation dans un maximum a taux = 2
