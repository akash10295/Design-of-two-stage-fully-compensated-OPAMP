# Design of Two-stage fully compensated OPAMP

This is one of my academic project from Spring 2018 semester.
Course: __EECT 6326: Analog Integrated Circuits Design__.
Professor: __Dr. Sudipto Chakraborty__.
In this course I got an introduction to the principles of analog IC design. I aquired the knowledge of circuit level analog IC design required in industry and research. With this knowledge, I designed an _Two stage Operational Amplifier with miller compensation and programmable nulling resistor_.

NOTE1:  I am going to skip the derivations of the formulas that I am using in this project. All these derivations can be found on the internet very easily. One of the source I would suggest is textbook by P. Allen and D. Holberg,"CMOS Analog Circuit Design",The Oxford Series in Electrical and Computer Engineering, 3rd ed.
NOTE2: You can go through this text or you can just refer the project report I made which is attached in the same repository.
NOTE3: The step numbers do not match with the numbers in images below. It is of least concern. The procedure follows a correct flow.


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
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/vth_ucox.jpg" />
</p>

I did DC Analysis on this setup. Once done I got the following values:

| Parameter                | NMOS             | PMOS           |
| ------------------------ |:----------------:| :-------------:|
| Threshold voltage        | Vtn_min = 0.52 V | /Vtp/ = 0.96 V |
|                          | Vtn_max = 0.96 V |                |
| Process transconductance | 200μA/V          |         60μA/v |

Now that we have the required unknowns, we can proceed to design stpes.

## 3. Deciding values of compensation capacitor (Cc) and bias current (I) from given load capacitor and Slew Rate.
The initial circuit for the system will be as shown below. I will make changes if thensystem doesn't meet the requred specifications.

<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Without%20nulling%20resistor.jpg" />
</p>

We have target Slew rate and given Load capacitor CL in the specification. We also have the target of Phase margin > 60 degree.
The condition for 60 degree phase margin is Cc>=0.22xCL Hence, for our project Cc should be more than or equal to 2.2pF. I am choosing value of Cc to **Cc = 3pF**
Now, SR = I5/Cc. From this we can calculate **I5 = SR x Cc = 30μA**.


## 4. Design of input transistors M1 and M2.
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Step%202.jpg" />
</p>

## 5. Design of mirror load transistors and tail current source transistor for first stage(M3, M4 and M5).
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Step%203.jpg" />
</p>

<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Step%204.jpg" />
</p>

Please keep a note that I have changed the sizes of input transistors from what we got initially. Therefore, the input transistor gm is also changed.


## 6. Design of second stage input transistor M6
Key things to keep in mind while designing 2nd input stage is that, it should properly mirror the current from first stage (blancing) and it should be sized in such a way that the output pole will go beyond our frequency of interests so that it will not create any concerns for us while designing.

<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Step%205a.jpg" />
</p>
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Step%205b.jpg" />
</p>

## 7. Design of current source transistor for second stage M7.
The current flowing from M6 will be same as the one flowing from M7. Als, M7 will form mirror with M5. Hench keeping that in mind, we have to size M7. Normally, S7 = 1/2x(S6)
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Step%206.jpg" />
</p>
---

Now we have all the W/L ratios of the transistors for the circuit we were aiming to build. When designed in cadence and plotted AC response by doing AC analysis we got following result.
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Schematic%20without%20nulling%20resistor.jpg" />
</p>

<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Plot%20Without%20Nulling%20Resistor.jpg" />
</p>

From the frequency response we can see that the phase margin that we got with this configuration is not what we expected. It is significantly low and we need make changes in the circuit.

## 8.Design of nulling resistor and its bias circuitary transistors.
As seen above, we did not get the required phase margin and we deciced to put the nulling resistor in series with the compensation capcitor. This can be implemented by using an ideal resistor but it is always a good pratice to try to design everything using MOS when designing IC. Based on the observed common mode signal at the output it is recommended to use a PMOS device (M8) to implement this resistor. The gate voltage for this PMOS can be anything which will make sure that it is turned on (even though there will not be any DC current flowing through it because of the capcitor in series). If we make this gate voltage fixed then this topology will work only for fixed load. To make it 'programmable' for any loads following arrangement can be made.
The following diagram also follows the calculations of aspect ratios of newly added transistors to the system (M8, M9, M10, M11)

<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/4.jpg" />
</p>
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/5.jpg" />
</p>
---

Once this this done, I made the corresponding changes in the previous circuit in cadence and simulated it.
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Schematic%20After%20inserting%20Nulling%20resistor.jpg" />
</p>

From above image, we can see that all the transistors are in saturation region which proves that we are going in right direction. After this I plotted the AC reponse of the circuit as shown below.
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Response%20after%20inserting%20nulling%20resistor.jpg" />
</p>

We can clearly see that the new __phase margin we got is 82 degree__ which is very excellent. The DC gain of the circuit is __Av(0)=Adm=65.57db__. Also the gain bandwidth is __GBW = 24MHz__.

I this way out OPAMP designing part is done. Now we have to test this OPAMP in various configuration to see if it is meeting other required specifications or not.

This procedure proceeds as follows:
### 1. Calculation of CMRR
We know that __CMRR(dB) = Adm(dB) - Acm(dB)__. We already have the value of Adm = 65.57dB. We now need to calculate the commo mode gain. This can calculated by doing following setup. Here I have given a common mode signal at the output and I have plotted a frequency response.
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Common%20mode%20gain%20setup.jpg" />
</p>
<p align="center">
<img src = "https://github.com/akash10295/Design-of-two-stage-fully-compensated-OPAMP/blob/master/Screenshots/Common%20mode%20gain%20plot.jpg" />
</p>

From the response we can see that the Acm = -15.36dB. Hence the CMRR is, __CMRR = Acm – Adm = 65.57 - (-15.36) = 80.9dB__, which is very excellent.
