# SIMULATION OF FREQUENCY DIVISION MULTIPLEXING (FDM) AND DEMULTIPLEXING USING SCILAB
### AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

### EQUIPMENTS Needed

Computer with Scilab installed

### ALGORITHM

Define six different frequencies to generate six sine wave signals.

Generate the time vector to represent time samples.

Compute six sine signals for each frequency over the time vector.

Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.

Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.

Plot original signals, multiplexed signal, and demultiplexed signals for verification.

### PROGRAM

```
t = linspace(0, 1, 1000);
fs = 1000;

freqs = [6 11 17 23 29 36];
amps = [1 2 3 4 5 6];

signals = zeros(6, length(t));
for i = 1:6
    signals(i,:) = amps(i) * sin(2*%pi*freqs(i)*t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i,:);
end

order = 50;
cutoff_freq = 10 / (fs/2);
h = ffilt("lp", order, cutoff_freq);

demux = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* sin(2*%pi*freqs(i)*t);
    demux(i,:) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t,signals(i,:));
    title("Original Signal f=" + string(freqs(i)));
    end

scf(2);
clf;
plot(t,fdm_signal);
title("FDM Signal");

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t,demux(i,:));
    title("Demultiplexed Signal f=" + string(freqs(i)));
end


```

### GRAPH:

<img width="1824" height="982" alt="image" src="https://github.com/user-attachments/assets/de0eb84b-c3e0-4ef3-81db-8d9855639c97" />
<img width="676" height="528" alt="image" src="https://github.com/user-attachments/assets/dfed70f3-c616-4bd2-b968-327f973d4ddb" />
<img width="1909" height="971" alt="image" src="https://github.com/user-attachments/assets/cb7b812e-8634-4190-b886-c42c17c13b83" />


### TABULATION:

![WhatsApp Image 2025-12-03 at 14 25 21_2476b00a](https://github.com/user-attachments/assets/bf7bea45-7c9d-4adb-ac43-95147faa318d)

![WhatsApp Image 2025-12-03 at 14 25 20_429b3951](https://github.com/user-attachments/assets/1515032a-5cea-4657-aaa4-25eab940d807)

### RESULTS:

The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.
