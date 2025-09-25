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
wp = 0.2*%pi;      // Passband frequency in radians
ws = 0.6*%pi;      // Stopband frequency in radians
alphap = 2;      // Passband attenuation in dB
alphas = 14;     // Stopband attenuation in dB
T = 1;           // Sampling time
omegap = (2/T) * tan(wp/2);
omegas = (2/T) * tan(ws/2);
N = log10( ((10^(0.1*alphas))-1) / ((10^(0.1*alphap))-1) ) / (2*log10(omegas/omegap));
N = ceil(N);

omegac = omegap / ((10^(0.1*alphap)-1)^(1/(2*N)));
hs = analpf(N, 'butt', [0, 0], omegac);
s = poly(0, 's');
h_analog_hpf = horner(hs, omegac ./ s);

z = poly(0, 'z');
Hz = horner(h_analog_hpf, (2/T)*((z-1)./(z+1)));
Hw = frmag(Hz, 512);
w = 0:%pi/511:%pi;
plot(w/%pi, abs(Hw));
xlabel('Normalized Digital Frequency (×π rad/sample)');
ylabel('Magnitude');
title('Butterworth Highpass IIR Filter Frequency Response');



## OUTPUT (LPF) : 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d79c2299-b790-4989-a1de-3ccbb1ebd351" />

## OUTPUT (HPF) : 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b39dd6fb-e546-4fca-9f2a-3a6e0655f0ff" />

## RESULT: 
The design of an IIR Butterworth filter using SCILAB is sucessfully completed.
