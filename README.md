# EXP 3A : IIR-BUTTERWORTH-FITER-DESIGN

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
13 
 
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
 
 
z=poly(0,'z');//Defining variable z 
 
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

clear;
clc;
close;

wp=input('Enter the pass band frequency (Radians )= ' ); 
ws=input('Enter the stop band frequency (Radians )= ' ); 
alphap=input( ' Enter the pass band attenuation (dB)=' ); 
alphas=input( ' Enter the stop band attenuation(dB)=' ); 
T=input('Enter the Value of sampling Time=');

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

```

## OUTPUT (LPF) : 
<img width="813" height="1135" alt="image" src="https://github.com/user-attachments/assets/a02cf4ca-59b0-4e02-b66a-10644c41c04b" />

<img width="928" height="884" alt="image" src="https://github.com/user-attachments/assets/1ebdff1b-fc0c-4962-a01f-7542e0f26964" />

## OUTPUT (HPF) : 
<img width="941" height="1116" alt="image" src="https://github.com/user-attachments/assets/75644e36-fedb-4624-ac0d-d3c312a589d2" />

## RESULT: 
Thus, design of Butterworth Low pass and High pass IIR filter waveforms were plotted and output was verified.
