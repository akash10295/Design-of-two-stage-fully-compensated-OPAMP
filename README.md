#### Design-of-two-stage-fully-compensated-OPAMP

This is one of my academic project from Spring 2018 semester. Course __EECT 6326: Analog Integrated Circuits Design__. In this course I got an introduction to the principles of analog IC design. I aquired the knowledge of circuit level analog IC design required in industry and research. With this knowledge, I designed an _Two stage Operational Amplifier with miller compensation and programmable nulling resistor_.

NOTE: You can go through this text or you can just refer the project report I made which is attached in the same repository.


The project flow goes as follows:
1. Declaring design specifications.
2. Getting values of threshold voltages (Vthn and |Vthp|) and process-transconductances for both PMOS and NMOS (μpCox and μnCox).
2. Deciding values of compensation capacitor (Cc) and bias current (I) from given load capacitor and Slew Rate.
3. Design of input transistors.
4. Design of mirror load transistors and tail current source transistor for first stage.
5. Design of second stage input transistor.
6. Design of current source transistor for second stage. (Once this it done, we will check the reponse of the OPAMP without nulling resistor. If needed, then)
7. Design of nulling resistor and its bias circuitary transistors.

So without delay, let's start designing!

## 1. Declaring design specifications.
We are required to design an OPAMP having load capacitor CL = 10pF with the 3.3 volts power supply. I used the TSMC CMOS 0.35-μm technology for this project. An OPAMP was designed to best meet the following specificatons:
- Differential voltage gain: Avd ≥ 60dB.
- Output voltage swing range: OVSR = Vo(max) -Vo(min) ≥ 2V.
- Slew rate: SR ≥ 10 V/μS.
- Input common mode range: ICMR ≥ 1.8V.
- Common mode rejection ratio: CMRR ≥ 70 dB.
- Unity Gain-bandwidth: GB ≥ 8 MHz with a 10 pF load capacitance.
- Phase Margin: f(GB) ≥ 60° with a 10 pF load capacitance.
- Power dissipation: Pdiss ≤ 1mW.

## 2. Deciding values of compensation capacitor (Cc) and bias current (I) from given load capacitor and Slew Rate.
