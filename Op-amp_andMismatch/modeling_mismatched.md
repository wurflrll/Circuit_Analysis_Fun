## MODELLING MISMATCHED TRANSISTORS (BJTs)

# Intro
In analog electronics at school, little emphasis is put on transistor mismatch, which can obviously have a drastic impact on our fundamental building blocks (current mirrors, all differential amplifiers, ect.)  I want to do a little bit of my own investigation into how we simulate mismatch, and so a goal is to make a decent operational amplifier (with transistor mismatch in mind).

## Basic Simulation
Before doing anything, I need to figure out how to simulate this in SPICE.  I can easily copy the parameters from a known transistor, I used the 2N2222, and change a few of the parameters.  The main parameter we think about that varies due to manufacturing inconsistencies is the DC current gain, $\beta$.  The default 2N2222 model used in LTSpice has a given $\beta$/BF of 200, but the transistor model means that the low current beta is half the given value.  So the 2N2222 would have $\beta = 100$ for $I_c < 5mA$, which is the region we will be operating in.  Analyzing mismatch on this level using the model of a discrete BJT is a little goofy (especially considering $\beta = 100$ is higher than the low current $\beta$ on the datasheet), but I mostly want to demonstrate some principles to myself.

To start, I create a duplicate model of the 2N2222, but changed BF to 80 (creating an effective $\beta$ of 40).  The original model I called "NPN_HIGHER" and the new model "NPN_LOWER".  



## Revisiting another parameter
Although $\beta$ varies between two BJTs of the same model, another important parameter is the saturation current (or scale current) $I_S.
The importance of $I_S$ can be chiefly found through the Eber-Moll Model:

To understand the relative importance of $I_S$ vs $\beta$, we could apply the Eber-Moll Model to the below circuit where the Eber-Moll model is given by the equation:

$I_c = I_s(e^{\frac{V_{BE}}{V_T}}-1)$

![VB applied to NPN with base and emitter resistor](images/colpitts_model.png)
*Note that $V_B$ is not simply the voltage at the base terminal.

From basic analysis we know:
$V_{BE} = V_B - I_BR_1 - I_CR_2$
and assuming active mode: $I_C = \betaI_{B}$

This parameter plays increased importance when the base resistor is 0 or small, when there is a strong base resistor present, the current is affected more by $\beta$