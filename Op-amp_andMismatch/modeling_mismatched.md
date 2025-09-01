## MODELLING MISMATCHED TRANSISTORS (BJTs)

# Intro
In analog electronics at school, little emphasis is put on transistor mismatch, which can obviously have a drastic impact on our fundamental building blocks (current mirrors, all differential amplifiers, ect.)  I want to do a little bit of my own investigation into how we simulate mismatch, and so a goal is to make a decent operational amplifier (with transistor mismatch in mind).

## Basic Simulation
Before doing anything, I need to figure out how to simulate this in SPICE.  I can easily copy the parameters from a known transistor, I used the 2N2222, and change a few of the parameters.  




With 500 ohms and matched = > 1.4 degree phase delay at 10kHz
1Mhz => 61 degree phase delay

1Mhz with mismatch => 33.4 degree


## Revisiting another parameter
Although $\beta$ varies between two BJTs of the same model, another important parameter is the saturation current (or scale current) $I_S.
The importance of $I_S$ can be chiefly found through the Eber-Moll Model:

$I_c = I_s(e^{\frac{V_{BE}}{V_T}}-1)$