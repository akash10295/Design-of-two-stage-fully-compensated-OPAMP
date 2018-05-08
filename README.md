# Design-of-two-stage-fully-compensated-OPAMP

This is one of my academic project from Spring 2018 semester. Course __EECT 6326: Analog Integrated Circuits Design__. In this course I got an introduction to the principles of analog IC design. I aquired the knowledge of circuit level analog IC design required in industry and research. With this knowledge, I designed an _Two stage Operational Amplifier with miller compensation and programmable nulling resistor_.

NOTE: You can go through this text or you can just refer the project report I made which is attached in the same repository.


The project flow goes as follows:
1. Declaring design specifications.
2. Deciding values of compensation capacitor (Cc) and bias current (I) from given load capacitor and Slew Rate.
3. Design of input transistors.
4. Design of mirror load transistors and tail current source transistor for first stage.
5. Design of second stage input transistor.
6. Design of current source transistor for second stage.
    Once this it done, we will check the reponse of the OPAMP without nulling resistor. If needed, then
7. Design of nulling resistor and its bias circuitary transistors.
