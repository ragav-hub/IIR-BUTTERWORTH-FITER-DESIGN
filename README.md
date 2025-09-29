# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
```
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

```

## PROGRAM (HPF): 
```
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


```

## OUTPUT (LPF) : 
<img width="1918" height="1199" alt="Screenshot 2025-09-29 161551" src="https://github.com/user-attachments/assets/3f61f789-e20b-4a5e-a245-f4ba6f18ebd7" />

<img width="1919" height="1199" alt="Screenshot 2025-09-29 161606" src="https://github.com/user-attachments/assets/1fc4b66d-b07f-4370-8a31-b21841401848" />

<img width="1919" height="1199" alt="Screenshot 2025-09-29 161526" src="https://github.com/user-attachments/assets/b7a9f799-26d2-49e9-ae3b-8c7c62cf7666" />


## OUTPUT (HPF) : 

<img width="1917" height="1198" alt="Screenshot 2025-09-29 161050" src="https://github.com/user-attachments/assets/37ba055d-7987-4d4f-b22f-c4cc48be151f" />

<img width="1919" height="1199" alt="Screenshot 2025-09-29 161103" src="https://github.com/user-attachments/assets/77866eb9-aed1-4d22-abfb-867108be82e8" />

<img width="1914" height="1191" alt="Screenshot 2025-09-29 161011" src="https://github.com/user-attachments/assets/1de6f594-55d8-44e3-9bfc-35103ca9547e" />

## RESULT: 
Thus, the design of an IIR Butterworth filter(LPF/HPF) using SCILAB is sucessfully executed and output is verified.
