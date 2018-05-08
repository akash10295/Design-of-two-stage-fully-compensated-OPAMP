#### Design-of-two-stage-fully-compensated-OPAMP

This is one of my academic project from Spring 2018 semester. Course __EECT 6326: Analog Integrated Circuits Design__. In this course I got an introduction to the principles of analog IC design. I aquired the knowledge of circuit level analog IC design required in industry and research. With this knowledge, I designed an _Two stage Operational Amplifier with miller compensation and programmable nulling resistor_.

NOTE: You can go through this text or you can just refer the project report I made which is attached in the same repository.


The project flow goes as follows:
1. Declaring design specifications.
2. Getting values of threshold voltages (Vthn and |Vthp|) and process-transconductances for both PMOS and NMOS (μpCox and μnCox).
3. Deciding values of compensation capacitor (Cc) and bias current (I) from given load capacitor and Slew Rate.
4. Design of input transistors.
5. Design of mirror load transistors and tail current source transistor for first stage.
6. Design of second stage input transistor.
7. Design of current source transistor for second stage. (Once this it done, we will check the reponse of the OPAMP without nulling resistor. If needed, then)
8. Design of nulling resistor and its bias circuitary transistors.

Once the design is complete, the circuit is tested for all the specification to confirm if it is working as the desired target specifications mentioned in step 1.

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

## 2. Getting values of threshold voltages (Vthn and |Vthp|) and process-transconductances for both PMOS and NMOS (μpCox and μnCox).
The most important parameters that we need during the calculation and which are not available with us imitially are threshold voltages and process trans conductances of the devices which we will be using throughout our designing. The only way to get them is by simulation. For that, I set up the NMOS and PMOS devices in diode connected fashion and forced 30μA of current through them with Vdd = 3.3 volts. The screenshot of this setup is as shown below.

<p align="center">
<img ![alt text](https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/vth_ucox.jpg)/>
</p>

With this setup I got the following values:

| Parameter                | NMOS             | PMOS           |
| ------------------------ |:----------------:| :-------------:|
| Threshold voltage        | Vtn_min = 0.52 V | /Vtp/ = 0.96 V |
|                          | Vtn_max = 0.96 V |                |
| Process transconductance | 200μA/V          |         60μA/v |
