[dft.js-playground](https://dirkarnez.github.io/dft.js-playground/)
===================================================================
Finally works (18 Dec 2025)
 
### Using
- [dft.js](https://github.com/dirkarnez/dft.js)

### TODOs
- [jsxgraph/jsxgraph: JSXGraph is a cross-browser library for interactive geometry, function plotting, charting, and data visualization in a web browser.](https://github.com/jsxgraph/jsxgraph)
- [ ] Minimum sampling frequency calculator (1 / (working hz *  sample size) = sampling frequency)
    - if do not have this, e.g. DFT will plot for example 198Hz / 202Hz for 200hz AC voltage, not good
    - 
- [ ] Ngspice
 - [ ] [eelab-dev/EEcircuit-engine: Simulation engine for EEcircuit](https://github.com/eelab-dev/EEcircuit-engine)
 - [ ] add audio voltage source
- [ ] Fundamental period calculation

### Notes
- How about sine wave of different amplitude over time?

### Testing data
- [`./data/EEsim.csv`](./data/EEsim.csv)
    - from [EEcircuit](https://eecircuit.com/)
        - `.tran tstep tstop <tstart <tmax>> <uic>`
        - [ngspice manual](https://ngspice.sourceforge.io/docs/ngspice-45-manual.pdf)
### SPICE
```
AC signal of 5 amplitude 200hz, 
Vin a 0 dc 0 ac 1 sin(0 5 200)
R1 a b 500
C1 b 0 10u
.tran 10u 0.02
*.ac dec 10 10 1000
.end
```
-  0.02 / (10*Math.pow(10, -6)) = 2000 samples

### Numpy
```python
import numpy as np

signal = [1, 2, 2, 0]

N = len(signal)
yf = np.fft.fft(signal)
xf = abs(np.fft.fftfreq(N, T)[:N//2])

print(yf)
print(xf)
```
```python
import numpy as np

# Create a sample signal (e.g., sum of two sine waves)
Fs = 1000 # sampling frequency
T = 1.0/Fs # sampling interval
t = np.arange(0, 1, T) # time vector
signal = np.sin(50 * 2.0 * np.pi * t) + np.sin(120 * 2.0 * np.pi * t)

# Compute the FFT
N = len(signal)
yf = [np.fft.fft(signal)]
xf = [np.fft.fftfreq(N, T)]

print(yf)
print(xf)
```
