# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
clc ;  

close ;  

wp=input('Enter the pass band frequency (Radians )= ' );  
ws=input('Enter the stop band frequency (Radians )= ' );  
alphap=input( ' Enter the pass band attenuation (dB)=' );  
alphas=input( ' Enter the stop band attenuation(dB)=' );  

T=input('Enter the Value of sampling Time='); 
omegap=(2/T)*tan(wp/2);  
disp(omegap,'omegap=');  
omegas=(2/T)*tan(ws/2);  
disp(omegas,'omegas=');    
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap));  
disp(N,'N='); 
N=ceil(N);  
disp(N,'Round off value of N=');  
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N)));  
disp(omegac,'omegac=');  
disp('Normalised Analog LPF Transfer function H(S)=');  
hs_Normalised = analpf(N,'butt',[0,0],1); 
disp(hs_Normalised);  
disp('Analog LPF Transfer function H(S)=');  
hs= analpf(N,'butt',[0,0],omegac);  
disp(hs);  
z=poly(0,'z'); 
Hz=horner(hs,(2/ T)*((z -1)/(z+1))) 
disp('Digital LPF Transfer function H(Z)=');  
disp(Hz);  
HW=frmag(Hz,512);  
w=0:%pi/511:%pi ;  
plot(w/%pi,abs(HW));  
xlabel(' Normalized Digital Frequency w');  
ylabel('Magnitude '); 
title(' Frequency Response of Butterworth IIR LPF');


## PROGRAM (HPF): 
clc;
close;
wp = input('Enter the pass band frequency (Radians )= ');
ws = input('Enter the stop band frequency (Radians )= ');
alphap = input('Enter the pass band attenuation (dB)= ');
alphas = input('Enter the stop band attenuation (dB)= ');
T = input('Enter the Value of sampling Time= ');

// Pre-warping (Bilinear Transformation)
omegap = (2/T) * tan(wp/2);
disp(omegap, 'omegap=');
omegas = (2/T) * tan(ws/2);
disp(omegas, 'omegas=');

// Order of the filter
N = log10(((10^(0.1*alphas))-1) / ((10^(0.1*alphap))-1)) / (2*log10(omegas/omegap));
disp(N,'N=');
N = ceil(N);
disp(N,'Round off value of N=');

// Cut off frequency
omegac = omegap / (((10^(0.1*alphap))-1)^(1/(2*N)));
disp(omegac,'omegac=');

// Normalised Analog LPF Transfer function
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);

// Analog LPF Transfer function
disp('Analog LPF Transfer function H(S)=');
hs = analpf(N,'butt',[0,0],omegac);
disp(hs);

s = poly(0,'s');
hpf_s = horner(hs, omegac/s);   // substitute s → omegac/s
disp('Analog HPF Transfer function H(S)=');
disp(hpf_s);

// Bilinear Transformation to Digital
z = poly(0,'z'); // Defining variable z
Hz = horner(hpf_s,(2/T)*((z-1)/(z+1))); 
disp('Digital HPF Transfer function H(Z)=');
disp(Hz);

// Frequency Response
HW = frmag(Hz,512);
w = 0:%pi/511:%pi;
plot(w/%pi, abs(HW));

xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude');
title(' Frequency Response of Butterworth IIR HPF');



## OUTPUT (LPF) : 
<img width="1918" height="1199" alt="495130043-3f61f789-e20b-4a5e-a245-f4ba6f18ebd7" src="https://github.com/user-attachments/assets/d63eb1b0-9d92-49aa-b655-1f3aba2bf5b0" />
<img width="1919" height="1199" alt="495130104-1fc4b66d-b07f-4370-8a31-b21841401848" src="https://github.com/user-attachments/assets/cf9fa039-1b1c-4cf1-bf3e-b5932e3452de" />
<img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/3e4b4a7f-a9c6-4ee2-84b5-47bb200ba1db" />


## OUTPUT (HPF) : 
<img width="1917" height="1198" alt="image" src="https://github.com/user-attachments/assets/852052ea-4fb5-4096-9a8b-922a4bef6701" />
<img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/5466c526-033c-435a-b57c-b01995727aab" />
<img width="1914" height="1191" alt="image" src="https://github.com/user-attachments/assets/6d0f3a22-9cd4-41ab-b86d-49dabb26e29c" />


## RESULT: 
Thus, the design of an IIR Butterworth filter(LPF/HPF) using SCILAB is sucessfully executed and output is verified.

