# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
clc; 
close;
wp=input('Enter the pass band frequency (Radians)= ' );
ws=input('Enter the stop band frequency (Radians)= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time='); 
omegap=(2/T)*tan(wp/2);
disp(omegap,'omegap='); 
omegas=(2/T)*tan(ws/2); 
disp(omegas,'omegas=');
N=log10(((10A(0.l*alphas))-1)/((10A(0.l*alphap))-1))/(2*log10(omegas/omegap)); 
disp(N,'N=');
N=ceil(N);
disp(N,'Round off value of N='); 
omegac=omegap/(((10A(0.l*alphap)) -l)A(l/(2* N))); 
disp(omegac,'omegac=');
disp('Normalised Analog LPF Transfer function H(S)=');
hs Normalised= analpf(N,'butt',[0,0],1); 
disp(hs_Normalised);
disp('Analog LPF Transfer function H(S)='); 
hs= analpf(N,'butt',[0,0],omegac); 
disp(hs);
z=poly(0,'z');
Hz=horner(hs,(2/ T)*((z -1)/(z+l))) 
disp('Digital LPF Transfer function H(Z)='); 
disp(Hz);
HW=frmag(Hz,512);
W=0:%pi/511:%pi;
plot(w/%pi,abs(HW));
xlabel(' Normalized Digital Frequency w'); 
ylabel('Magnitude ');
title(' Frequency Response of Butterworth IIR LPF');


## PROGRAM (HPF): 

clc; 
close;
wp = 0.2*%pi;	
ws = 0.6*%pi;
alphap = 2;
alphas= 14;
T = 1;

omegap = (2/T) * tan(wp/2); 
omegas= (2/T) * tan(ws/2);

N = log10( ((10A(0.l*alphas))-1) / ((10A(0.l*alphap))-1) ) / (2*log10(omegas/omegap));
N = ceil(N);

omegac = omegap / ((10A(0.l*alphap)-l)A(l/(2*N)));
hs = analpf(N, 'butt', [0, 0], omegac);
s = poly(0, 's');
h_analog_hpf = horner(hs, omegac ./ s);
z = poly(0, 'z');
Hz= horner(h_analog_hpf, (2/T)*((z-1)./(z+l)));
Hw = frmag(Hz, 512);
w = 0:%pi/511:%pi;
plot(w/%pi, abs(Hw));
xlabel('Normalized Digital Frequency (xn	rad/sample)'); 
ylabel('Magnitude');
title('Butterworth Highpass IIR Filter Frequency Response');

## OUTPUT (LPF) : 

## OUTPUT (HPF) : 

## RESULT: 
