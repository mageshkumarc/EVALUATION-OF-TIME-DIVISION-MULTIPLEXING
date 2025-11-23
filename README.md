# SIMULATION-OF-FREQUENCY-DIVISION-MULTIPLEXING-FDM-AND-DEMULTIPLEXING-USING-SCILAB



### AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.  

### EQUIPMENTS Needed

Computer with Scilab installed  

### ALGORITHM

1.Define six different frequencies to generate six sine wave signals.  
2.Generate the time vector to represent time samples.  
3.Compute six sine signals for each frequency over the time vector.  
4.Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.  
5.Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.  
6.Plot original signals, multiplexed signal, and demultiplexed signals for verification.  

### PROCEDURE
  Refer Algorithms and write code for the experiment.  
  • Open SCILAB in System  
  • Type your code in New Editor  
  • Save the file  
  • Execute the code  
  • If any Error, correct it in code and execute again  
  • Verify the generated waveform using Tabulation and Model Waveform  
  
### PROGRAM

```
t = linspace(0, 1, 1000);
fs = 1000; 

freqs = [4, 8, 12, 16, 20, 24];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;
cutoff_freq = 8 / (fs/2); 
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* sin(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2);
clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end

```
-
### TABULATION:
![WhatsApp Image 2025-11-23 at 11 58 15_d8626f05](https://github.com/user-attachments/assets/4eb606d6-489b-48b3-96eb-137aaa8671fb)

![WhatsApp Image 2025-11-23 at 11 58 15_20096c5a](https://github.com/user-attachments/assets/3f066aa3-4e0c-4555-aba5-78a7e6bc0ed3)


### GRAPH:
<img width="1919" height="999" alt="AC EXP111" src="https://github.com/user-attachments/assets/6468f9ba-a574-45bc-80e4-bdda96c0f3ca" />

<img width="1651" height="919" alt="AC EXP112" src="https://github.com/user-attachments/assets/49f2c3c8-8dbc-40c9-b0dd-827a4f004b64" />

<img width="1917" height="1001" alt="AC EXP 113" src="https://github.com/user-attachments/assets/3a22bc4c-0842-4655-9e21-a6ca094d063b" />

### RESULT:
The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.
