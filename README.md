[dft.js-playground](https://dirkarnez.github.io/dft.js-playground/)
===================================================================
Finally works (18 Dec 2025)
 
### Using
- [dft.js](https://github.com/dirkarnez/dft.js)

### TODOs
- [jsxgraph/jsxgraph: JSXGraph is a cross-browser library for interactive geometry, function plotting, charting, and data visualization in a web browser.](https://github.com/jsxgraph/jsxgraph)
- [ ] Minimum sampling frequency calculator (1 / (working hz *  sample size) = sampling frequency)
    - if do not have this, e.g. DFT will plot for example 198Hz / 202Hz for 200hz AC voltage, not good
- [ ] Ngspice audio plguin

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
