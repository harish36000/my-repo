# Operational Amplifier


### Why?

1. In 1940s, basic op-amp circuits were constructed using vacuum tubes to perform mathematical operations such as addition, subtraction, multiplication, division, differentiation, and integration.

2. Found in signal conditioners and filters

   **Signal Conditioners**: Signal conditioners take the analog signal from the sensor, manipulate it, and send it to the ADC (analog-to-digital converter) subsystem to be digitized for further processing (usually by computer software). For example, thermocouple signals have very small voltage levels that must be amplified before they can be digitized.

   **Filters**:

### What?

- Voltage amplifying device
- Active Component: Makes use if external power source to add power to the system. Other eg: vacuum tubes, transistors.
- Can perform a variety of different operations, giving rise to its name of “Operational Amplifier”.
- Three-terminal device 
- `+` is referred to as the noninverting input, and the  `-` marked terminal is called the inverting input.

### Basics:

### Active vs Passive

- The active component requires an external source for the operation, whereas the passive components do not require any external source for the operations.

- Active components are those who delivers or **produce energy** or power in the form of a voltage or current. Passive components are those who **utilises or store energy** in the form of voltage or current.
- Examples of the passive components are resistor, capacitor and inductor.
- Examples of the active components are op-amp, JFET- transistors.



## Ideal OP-AMP Characteristics

```c++
1. Input currents are zero
2. Two  Op-Amp Inputs have the same voltage
```

*NOTE: This does not mean that the two inputs are physically shorted together, and we should be careful not to make such an assumption. Rather, the two input voltages simply track each other: if we try to change the voltage at one pin, the other pin will be driven by internal circuitry to the same value*



## Inverting Amplifier

- `-` is connected to Vin
- `+` is connected to ground

```c++
Vout = -(Rf/R1)Vin
```

- If `Rf > R1` -> Amplification
- If `Rf < R1` -> Attenuation

- The current labeled `i`  **flows only through the two resistors R1 and Rf**; ideal op amp rule 1 states that no current flows into the inverting input terminal.

- Works for AC and DC inputs
- Changes the polarity
- V_out and V_in are out-of-phase



## Non-Inverting Amplifier

- `-` is connected to ground
- `+` is connected to Vin
- (actually not so directly opposite, check  R1 connection!)

```c++
Vout = (1 + Rf/R1)Vin
```

- Works for AC and DC inputs
- V_out and V_in are in-phase



## Voltage Follower

```c++
Vout = Vin
```

- Special case of noninverting amplifier where
  - R1 = ∞ 
  - Rf = 0
- The voltage follower draws no current from the input
- "save the current of first circuit form the ill effects of second circuit"

## Summing Amplifier

```c++
Vout = (-Rf)(V1/R1 + V2/R2 + V3/R3)
   
if R1=R2=R3=R,
Vout = (-Rf/R)(V1 + V2 + V3)
```

***Caution!*** (useful while solving Numericals)

*It is frequently tempting to assume that the current labeled `i`  flows not only through Rf but through RL also. Not true!* 

*It is very possible that current is flowing through the output terminal of the op amp as well, so that the currents through the two resistors are not the same. It is for this reason that we almost universally **avoid writing KCL equations at the output pin of an op amp**, which leads to the preference of nodal over mesh analysis when working with most op amp circuits.*

Refer Q12

## Difference Amplifier



## Cascaded Stages

A cascade connection is a head-to-tail arrangement of two or more op amp circuits such that the output of one is the input of the next. When op amp circuits are cascaded, each circuit in the string is called a **stage**.

Eg:

- 2-stage op-amp circuit

  - Stage 1: Summming Amplifier
  - Stage 2: Inverting Amplifier

- Together we have a summing amplifier that **does not invert the output** (no phase reversal)

  ```c++
  							V_out = (R2/R1)(Rf/R)(V1+V)
  ```

  

## Reliable Voltage Source

### Prerequisites:

#### Diode

1. Current flows in only one direction

2. Sine wave ->(through diode) only positive half cycle (rectification by diode)

3. ![image-20210109090844064](C:\Users\Harish\AppData\Roaming\Typora\typora-user-images\image-20210109090844064.png)

4. anode: p type (+)

   cathode: n type (-)

5. more number of electrons -> n type

   more number of holes -> p type

6. current direction -> p -to- n

7. Forward Bias - p type to positive of battery(i flow)

   Reverse          - n type to positive of battery(i blocked)


#### Zener Diode

1. Has asymmetric current-voltage relationship

   > Resistors have symmetric  current-voltage relationship

2. A Zener diode is a special type of diode designed to be used with a positive voltage at the cathode with respect to the anode; when connected this way, the diode is said to be **reverse biased**

3. In reverse bias,

   - `V_source >= V_z `
     - V across zener becomes constant
     - current flows
     - voltage clamps across diode
   - `V_source < V_z`: no current

   

### Voltage Source

![image-20210121162012589](C:\Users\Harish\AppData\Roaming\Typora\typora-user-images\image-20210121162012589.png)

The current supplied to R<sub>L</sub> does not depend on its resistance—the primary attribute of an ideal current source.

### Current Source

![image-20210121162133325](C:\Users\Harish\AppData\Roaming\Typora\typora-user-images\image-20210121162133325.png)











## Practical Considerations

### A More Detailed Op-Amp Model

|     Parameter     |  Ideal   | Practical |
| :---------------: | :------: | --------- |
| input resistance  | Infinite | Finite    |
| output resistance |   Zero   | Nonzero   |
|  open-loop gain   | Infinite | Finite    |

```c++
V_out = Av_d - Ro*i_out
```



- In simple words, op-amp can be defined as a voltage-controlled dependent voltage source

- Open loop Gain: the gain of the opamp component all by itself, with all other components removed. In particular, with the feedback components removed. The parameter `A` is referred to as the **open-loop voltage gain** of the op amp, and is typically in the range of 10^5 to 10^6.  

- Unit: V/V

- Open-loop voltage gain is a property of op-amp.

- Closed loop Gain:  the gain of the (amplifier circuit as a whole), from circuit-input to circuit-output, with all components intact. In particular, with the feedback components in place.

  The “loop” in this case refers to an external path between the output pin and the inverting input pin.

- Closed-loop voltage gain is a characteristic of op-amp circuit.



### Derivation of Ideal Op-Amp Rules

*Rule 1: Two Op-Amp Inputs have the same voltage*

- <u>Differential Input Voltage</u> (Vd)

  ​							`Vd = Vout/A`

- An ideal op amp would have **infinite open-loop gain**, resulting in `Vd = 0`

*Rule 2: Input Currents are zero*

- <u>Input Bias Current</u> (i_in)

  ​							`i_in=Vd/Ri`

- As the input voltage(Vd) has a negligible value, we can say i_in also tends to 0



### Common Mode Rejection

- The op amp is occasionally referred to as a *difference amplifier*, since the output is proportional to the voltage difference between the two input

- If v1 = 2 + 3 sin 3t volts and v2 = 2 volts, we would expect the output to be −3 sin 3t volts; the 2 V component *common* to v1 and v2 would not be amplified, nor does it appear in the output.

- For practical op amps, we do in fact find a small contribution to the output in response to common-mode signals. In order to compare one op amp type to another, it is often helpful to express the ability of an op amp to reject common-mode signals through a parameter known as the **common-mode rejection ratio**, or CMRR.

```c++
  			  Acm  = |Vocm/Vcm|	  (Acm=common mode gain; Vocm =output V when V1=V2=Vcm)
              CMRR = |A/Acm|      (A=differential mode gain, V/V gain unit)
              CMRR in dB= 20log|A/Acm| dB
```

> log here is log<sub>10</sub>



### Circuit Feedback

#### Negative Feedback

The negative feedback configuration aims at minimizing the potential difference vd between the inverting and non-inverting inputs of the operational amplifier

Negative feedback also provides **increased stability** in situations where A is sensitive to the op amp’s
surroundings. For example, if A suddenly increases in response to a change in the ambient temperature, a larger feedback voltage is added to the inverting input. This acts to <u>reduce the differential input voltag</u>e vd, and therefore the change in output voltage `AV_d` is smaller

> ***Closed-loop circuit gain is always less than the open-loop device gain***

#### Positive Feedback

Things may blow up. Amplitude increases after every iteration.



### Saturation

> Linear Device: Devices that are independent of the way in which it is connected in a circuit.

Saturation effects occur when any part of a feedback control system *reaches a physical limit*. These limits can have many forms: a spring that is compressed to the limit.

For an operational amplifier saturation is when the **output voltage is limited to the supply voltage**

For example, if we choose to run the op amp with a +9 V supply and a −5 V supply, then our output voltage will be limited to the range of −5 to +9 V. 

The output of the op amp is a linear response bounded by the positive and negative saturation regions, and as a general rule, we try to design our op amp circuits so that we do not accidentally enter the saturation region

"Saturation happens in non-linear range. Usable in linear range."

### Offset Voltage

There is a tendency for real op amps to have a nonzero output even when the two input terminals are shorted/0V together. The value of the output under such conditions is known as the **offset voltage**, and the input voltage required to reduce the output to zero is referred to as the **input offset ** **voltage**

<u>Offset Null Pin</u>: 

Most op amps are provided with two pins marked either “offset null” or “balance.” These terminals can be used to adjust the output voltage by connecting them to a variable resistor.

"Give some supply voltage, to change offset and make it 0 externally"

### Slew Rate

The rate at which the output voltage can respond to changes in the input. It is most often expressed in V/μs



### Packaging

Modern op amps are available in a number of different types of packages. Some styles are better suited to high temperatures, and there are a variety of different ways to mount ICs on printed-circuit boards. 

The label “NC” next to a pin means “no connection.”



## Comparators 

>"If the circuit features an electrical connection between the output pin and the inverting input pin.  This is known as closed-loop operation, and is used to provide negative feedback..."

- Comparators are op amps designed to be driven into saturation. 
- These circuits operate in open loop, and hence have no external feedback resistor.

*Notice how there is no closed loop(feedback) in the circuit diagram for comparator. Hence it uses open-loop configuration*

Let's assume source to be 12V. Then,

|     Parameters      |  Inverting(in-text)   |     Non Inverting     |
| :-----------------: | :-------------------: | :-------------------: |
| 1. Input Pin (V_in) |           -           |           +           |
|   2. V_in < V_ref   | +12 V (positive sat.) | -12 V (negative sat.) |
|   3. V_in > V_ref   |         -12 V         |         +12 V         |

*"Only amplifier circuit, where output is not proportional to the input"*

We can say that the voltage comparator is essentially a **1-bit analogue to digital converter**, as the input signal is analogue but the output behaves digitally.



##  Instrumentation Amplifier

Instrumentation Amplifiers are basically used to amplify small differential signals. Eg: low-frequency signals (≪1 MHz), low voltage signals(in order of millivolts), signals produced by thermocouples or strain gauges.

"Has very good CMRR"

A 3 op-amp instrumentation amplifier is made of 2 buffer and 1 difference amplifier.

*All derivations for inst. amplifier are made assuming all 3 are ideal op-amps*

In order to maximize the CMRR of the instrumentation amplifier, we expect
`R4/R3 = R2/R1`

```c++
				Vout = (R4/R3)(1+(R2/R1)/(1+R4/R3))V+ - (R2/R1)V- 
```



### Virtual Ground

![image-20210112075049861](C:\Users\Harish\AppData\Roaming\Typora\typora-user-images\image-20210112075049861.png)

 A **virtual ground** (or **virtual earth**) is a node of a circuit that is maintained at a steady reference potential, without being connected directly to the reference potential.

Above concept is valid only when **negative feedback** is applied to opamp like in inverting amplifiers.



## Floating Output

Opamp outputs are never floating, feedback resistor or not. Their outputs are driven to match what the inputs tell them to do, if that's possible, or driven to one or the other power supply. In no case are they floating. So it is always OK to leave an opamp output unconnected. The feedback resistor is driven by the output; the output is not held in place by the feedback resistor.

## Commonly Used Terms (from lectures)

1. Gain

   ![image-20210123100318400](C:\Users\Harish\AppData\Roaming\Typora\typora-user-images\image-20210123100318400.png)

2. Active and Passive Components

3. Floating Output: (in opamp output is never floating)

4. Reliable Voltage and Current Source

5. Q12 Analyze the circuit of Fig. 6.42 and determine a value for
   V1, which is referenced to ground.

6. Q17, negative answers, current flow
