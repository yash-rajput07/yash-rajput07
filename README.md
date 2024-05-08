Expt - Simulation program to study effect of ISI and noise in baseband communication 
system. 
%pnrz.m
function pout=prect(T);
pout=ones(1,T);
end
%prz.m
function pout=prect(T);
pout=[zeros(1,T/4) ones(1,T/2) zeros(1,T/4)];
end
%psine.m
function pout=psine(T);
pout=sin(pi*[0:T-1]/T);
end
%prcos.m
function y=prcos(rollfac,length,T)
y=rcosfir(rollfac,length,T,1,'normal');
end
%binary_eye.m
clear;clf;
data=sign(randn(1,400));%generate 400 random bits
Tau=64;
dataup=upsample(data, Tau);%generate impulse train
yrz=conv(dataup,prz(Tau));
yrz=yrz(1:end-Tau+1);
ynrz=conv(dataup,pnrz(Tau));
ynrz=ynrz(1:end-Tau+1);
ysine=conv(dataup,psine(Tau));
ysine=ysine(1:end-Tau+1);
Td=4;
yrcos=conv(dataup,prcos(0.5,Td,Tau));
yrcos=yrcos(2*Td*Tau:end-2*Td*Tau+1);
eye1=eyediagram(yrz,2*Tau,Tau,Tau/2);
title('RZ Eye-Diagram');
eye2=eyediagram(ynrz,2*Tau,Tau,Tau/2);
title('NRZ Eye-Diagram');
eye3=eyediagram(ysine,2*Tau,Tau,Tau/2);
title('HALF SINE Eye-Diagram');
eye4=eyediagram(yrcos,2*Tau,Tau);
title('Raised COSINE Eye-Diagram');
[MCOE - PCS - Expt Programs - Eye-Diagram- SNR - PCM and DM- Sampling theorem (1).pdf](https://github.com/yash-rajput07/yash-rajput07/files/15244138/MCOE.-.PCS.-.Expt.Programs.-.Eye-Diagram-.SNR.-.PCM.and.DM-.Sampling.theorem.1.pdf)
