 # CMOS-Circuit-Design-SPICE-Simulation-using-Sky130nm-technology
---
&copy; saikrupas 

## Table Of Contents :-
---
- [NgspiceSky130-Day1-Basics of NMOS Drain Current(Id) vs Drain-to-source Voltage(Vds)](#NgspiceSky130-Day1-Basics-of-NMOS-Drain-Current(Id)-vs-Drain-to-source-Voltage(Vds))

  - [TOPIC-1:-Introduction to Circuit Design and Spice Simulations](#topic-1--introduction-to-circuit-design-and-spice-simulations)
    - [LECTURE-1-Why do we need SPICE simulations?](#lecture-1--why-do-we-need-spice-simulations)
    - [LECTURE-2-Introduction to basic element in circuit design-NMOS](#lecture-2--introduction-to-basic-element-in-circuit-design-nmos)
    - [LECTURE-3-Strong inversion and threshold voltage](#lecture-3--strong-inversion-and-threshold-voltage)
    - [LECTURE-4-Threshold voltage with positive substrate potential](#lecture-4--threshold-voltage-with-positive-substrate-potential)
  - [TOPIC-2:-NMOS resistive region and Saturation region of operation](#NMOS-resistive-region-and-Saturation-region-of-operation)
    - [LECTURE-1-Resistive region of operation with small drain-source voltage](#lecture-1-resistive-region-of-operation-with-small-drain-source-voltage)
    - [LECTURE-2-Drift current theory](#lecture-2-drift-current-theory)
    - [LECTURE-3-Drain current model for Linear region of operation](#lecture-3-drain-current-model-for-linear-region-of-operation)
    - [LECTURE-4-SPICE conclusion to resistive operation](#lecture-4-spice-conclusion-to-resistive-operation)
    - [LECTURE-5-Pinch-off region condition](#L5-Pinch-off-region-condition)
    - [LECTURE-6-Drain current model for saturation region of operation](#L6-Drain-current-model-for-saturation-region-of-operation)
  - [TOPIC-3:-Introduction to SPICE](#Introduction-to-SPICE)
    - [L1 Basic SPICE setup](#L1-Basic-SPICE-setup)
    - [L2 Circuit description in SPICE syntax](#L2-Circuit-description-in-SPICE-syntax)
    - [L3 Define Technology parameters](#L3-Define-Technology-parameters)
    - [L4 First SPICE simulation](#L4-First-SPICE-simulation)
    - [L5 SPICE lab with Sky130 models](#L5-SPICE-lab-with-Sky130-models)

---
# NgspiceSky130-Day1-Basics of NMOS Drain Current(Id) vs Drain-to-source Voltage(Vds)

## <u>Topic-1 :-Introduction to Circuit Design and Spice Simulations</u>

### <u>Lecture-1:- Why do we need SPICE simulations?</u> 
#### <u>Circuit design and SPICE simulation </u></br>
A circuit design includes PMOS and NMOS tied together in a particular fashion so that they result into logic gates such as NAND, NOR, OR, AND etc.</br>

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-1.png?raw=true"/>

The above is an inverter it has an PMOS transistor and an NMOS transistor, the drains(D) of both the transistors are connected together, the gates(G) of both are tied together and this kind of connection fashion of NMOS and PMOS transistors gives the functionality of an inverter.</br>
Similarly,we will have a bunch of PMOS at the top and NMOS at the bottom to give the functionality of NAND,NOR or any kind of gates. So the <u>circuit design</u> determines what kind of PMOS and NMOS transistors needs to be connected in a certain fashion to provide a particular functionality.</br>
<u>SPICE simulation</u> is basically to provide some  waveforms to a circuit to identify the output characteristics.</br>

The above inverter will have the following charactersitics, they basically describe the NMOS and PMOS transistors and basically it desides the delay of the particular cell.So based on the delay value we can actually tune the  W/L ratio of the transistors.The W/L ratio desides the value of the currents and these values will deside the waveform shape further this shape desides the delays of a particular cell.</br>
So, we do SPICE simulations to tune the delay and we will get the W/L ratio of that particular transistor.</br>
#### Tune the delay <---> tune the W/L ratio </br>

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-2.png?raw=true"/>

**Why do we need SPICE?**</br>
The clock Tree synthesis, crosstalks, and timing are built on SPICE (Simulation Program with Integrated Circuit Emphasis), without SPICE there won't be any delays and if there are no delays clock tree, physical design flow, crosstalk dosen't make any sense.</br>

Let us say we have done some Clock Tree Synthesis of the circuit shown below with bufffers with different specifications ( type-1 and type-2 buffers) with different capacitive load at the output.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-5.png?raw=true"/>

After the SPICE simulation we get a "Delay Table", which includes input slew and output load. The intersection value of Input slew and Output load is considered as <u>Delay</u>. Delay tables for both level 1 and level 2 buffers have been shown in the below image. This is calculated by circuit design and SPICE simulation.</br>.
The delay values of type 1 and type 2 buffers have different values becaues  both the buffers might be made up of different PMOS and NMOS transistors.</br>
In reality, every PMOS and NMOS transistor differs form near by transistors.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-6.png?raw=true" />

The Cbuf1 and Cbuf2 will have different W/L ratios. These values are obtained from circuit design.</br> 
The source of the above values in the Delay Tables comes from circuit design using SPICE simulations. SPICE simulations involves characterisation of any CMOS logic into detail.</br>

------

### <u>Lecture-2:- Introduction to basic element in circuit design-NMOS</u>
A NMOS is a 4-terminal device with gate,source,drain and body as its terminals.The NMOS means <u>N-channel MOS transistor</u> (metal oxide semiconductor).</br>
The NMOS transistor consist of P-type substrate (Sub), with heavily doped with n+ region. There are two isolated regions made up of SiO2 which acts an insulator therefore isolates the transistor from other transistors . The n+ regions acts as diffusion regions and denotes Source (S) and Drain (D) respectively. Above it there gate oxide layer, and top of it has a poly-Si / metal gate deposition which acts as the Gate (G) termianal.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-7.png?raw=true"/>

**Threshold Voltage (Vt)**</br>
This is a very important term, all the characterisation depends on threshold voltage.</br>
At first we will keep the Vgs=0, means source and drain terminals both are grounded. Body is also grounded. P-substrate and n+ act as PN junction diode and as there is no potential so there is a high resistance. No channel formation is there.</br>


<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-8.png?raw=true" />

Now, if we will apply a small positive  potential at Vgs>0. We will observe  positive charge accumulation  at the gate terminal and as a result of this the negative charges stars to accumulate at the surface of the substrate.</br>
The positively charges starts to repel towards the interiors of the P-substrate leaving behind negative charges.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-9.png?raw=true" /></br>

The ones that are left behind are the negative charges.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-10.png?raw=true"/>

-----

### <u>Lecture-3:- Strong inversion and threshold voltage</u>

Due to Accumulation of negatuve charges, there will be formation of Depletion Region, depleting of it's majority carriers i.e positive carriers here.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-11.png?raw=true"/></br>
<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-12.png?raw=true"/>

Now, we will gradually increase the  Gate voltage (Vgs) further, we will see that the positive charge carriers will be repelled and there will be increase of Depletion Width. On further increase of Gate voltage (Vgs) we will reach a point where the small surface of P-substrate gets inverted into an n-type material/surface completely, this is called <u>"Surface Inversion" or "Strong Inversion".</u> The gate voltage (Vgs) where Strong Inversion happens is called <u>"Threshold Voltage (Vt)"</u>.</br>

**<u>The gate voltage (Vgs) at which the strong inversion / surface inversion happens is referred as the Threshold voltage (Vt)**</u></br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-14.png?raw=true"/>

**What will happen if we further increase the gate voltage (Vgs)?**</br>
 As there are no more negative charges that will be attracted towards the positive gate voltage(Vgs), The negative charges from n+ regions will get attracted and threfore the channel width gets increased resulting in the  formation of channel at the surface but the depletion region width remains unchanged.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-15.png?raw=true"/></br>

Now there is a possibility of current flow from Source to Drain. The channel has bridged the gap between source to drain regions. But as there is no Drain voltage so the elctrons will not move, This region of operation of NMOS transistor is called as the <u>Cut-off region</u>.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-16.png?raw=true"/>

We will see what happens when we apply  potential at the Body terminal.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-17.png?raw=true"/></br>

So when we apply a positive potential to the source-to-body terminal ie, Vsb.The source to body area gets additional reverse biased.
This will result in the increase of the depletion region width between source and body terminal. </br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-18.png?raw=true"/></br>
<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-19.png?raw=true"/></br>
<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-20.png?raw=true"/></br>

------

### <u>Lecture-4:- Threshold voltage with positive substrate potential</u>

If we increase Vgs, we will see that the depletion region width increase in both the cases. But, in second case as there is Vsb +ve, few charges from the channel will get pulled towards the source.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-21.png?raw=true"/></br>

Due to this phenomena the surface inversion will be slower in second case. Therefore some extra potential has to be apllied in second case to create surface inversion.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-22.png?raw=true"/></br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-23.png?raw=true"/></br>

In the presence of substrate bias (Vsb), an additional potential is required for strong inversion.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-24.png?raw=true"/></br>

The parameters such as Gamma(body effect coefficient) comes from the technology parameters or the device parameters(doping concentration of p-substrate/n+ region).These values are all constants that comes from the foundry,these constants are termed as models and these constant values  are feed to the SPICE simulator will derive the Threshold voltage out of these values and this threshold voltage (Vt), will represent a particular requirement of device (NMOS or PMOS).</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-25.png?raw=true"/></br>

-----
-----

## <u>Topic-2 :-NMOS resistive region and Saturation region of operation</u>

### <u>Lecture-1:-Resistive region of operation with small drain-source voltage</u>

Previously, we learned about the  Cut Off region of operation of the MOSFET, now we will see the <u>"Resistive region"/"Linear Region"</u> of operation of MOSFET, by applying Drain-source voltage.

In the below image, when Vgs=vt is the voltage at which the <u> strong inversion</u> occurs and this voltage is termed as the <u> threshold voltage (Vt).</u>Therefore, the P type surface gets converted completely into a N-type material.</br>

<img width="1305" height="508" alt="image" src= "https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-26.png?raw=true"></br>

As Vgs=Vt,now if we keep on increasing the Gate-source voltage(Vgs) than (Vt), ie.(Vgs>Vt),the charge carries increases in the channel region thus the channel width keeps on increasing between soucre and drain region.</br>

<img width="1305" height="508" alt="image" src= "https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-27.png?raw=true">

<img width="1305" height="508" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-28.png?raw=true"></br>

**<u>Resistive Operation of NMOS**</u></br>

As the value of Vgs voltage increses more than Vt <u>(Vgs>Vt)</u>, the accumulation of the charge carriers increases in the channel region, resulting to larger conducting area between source and drain.</br>
As the value of Vgs increase from 1v,1.5v,2v,2.5v, it refers to <u> the induced charges (Qi) is proportional to the gate voltage (Vgs)</u>.</br>

> (Qi) = (Vgs - Vt)

<img width="1305" height="508" alt="image" src= "https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-29.png?raw=true"></br>

so, (Vgs - Vt) is basically the potential to turn on the transistor.</br>
 
 Now,let's apply very small drain-source voltage (Vds) (Vds=0.05v).By keeping the Vgs=1V and the is Vt=0.5v.
 The value of Vgs>Vt following the transistor to turn ON(conducting channel between source-drain).</br>

<img width="1305" height="508" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-30.png?raw=true"></br>

Now,as we can see the source is grounded and the drain is connected to Vds.
Ideally, if we observe the source is at 0 potential and the source is at Vds potential,so there will be a voltage gradient across the channel ie. the voltage is not constant all over the channel.</br>

<img width="1305" height="508" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-31.png?raw=true"></br>

If you look the effective channel length(L), the difference between the channel length and effective channel length is the one that we get after process.</br>
The effective channel length is much lesser than the actual channel length.Because of the fabrication techniques.</br>

<img width="1305" height="508" alt="image" src= "https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-32.png?raw=true"></br>

The x-axis represents the effective channel length (L).</br>

<img width="1305" height="508" alt="image" src= "https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-32.png?raw=true"></br>

Here, y-axis represents the width of transistor and x-axis represents the voltage across the channel.</br>
On applying Vds, every point on x-axis(along the length of the channel) will vary w.r.t to Vgs-V(x),so the effective channel voltage/ gate to channel voltage on the application of Vgs will be:-</br>

> Effective channel voltage (on the application of Vds) = Vgs - V(x)</br>

 This will lead to the current flow and this will decide the current flow equation.</br>

<img width="1305" height="508" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-34.png?raw=true"></br>

-----

### <u>Lecture-2:-Drift current theory</u>

Till now we know that effective channel voltage will vary w.r.t x so effective voltage is <u>Vgs-V(x)</u>, for example at x=0, Vgs=1V and V(x)=0, the Vgs-V(x)=1V. At V(x)=Vds=0.05V, the Vgs=1V Vgs-V(x)=0.95V. The voltage across the channel will lies between 1V to 0.95V so the channel voltage is not constant its a  gradient because of the presence of Vds.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-35.png?raw=true"></br>

The amount of induced charges in the channel in the presence of Vds. The charge which is induced in the channel is proportional to the Vgs-V(x) which is the effective voltage at each and every point in the channel. </br>
Now, in the induced chagre equation, it is proportional to the effective channel voltage.</br>
Basically, the induced charge at every point is,</br>
>Q = C . V (charge conservation principle)

Here, Cox is the gate oxide capacitance.

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-36.png?raw=true"></br>

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-37.png?raw=true"></br>

So, with this above formula of charge lets derive the current equations. Because current is the function of charges in the channel.</br>

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-38.png?raw=true"></br>

The above values are constants which are given by the foundary and the technology node used.</br>

There are two types of currents:-</br>

 <u>Dift current</u>- current due to the differnce in th potential differnce.</br>
 <u>Diffusion current</u> - current due to the variation of charge carrier concentration.</br>
 Here there is Drift current as there is a potential difference across the effective channel.</br>

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-38.png?raw=true"/></br>

To get the drain current(Id), which is the current due to the difference in the potential (drift current), we will see the top view of transistor to measure the drain current.</br>

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-39.png?raw=true"></br>

------

### <u>Lecture-3:-Drain current model for Linear region of operation</u>

Till now we know that the  drain current (Id), is the product of velocity of charge carriers with available charge over the channel width.</br> 

As there is change of voltage across the channel length, which will result in change of velocity of charge carriers which is a function of mobility and electrci field.The value of mobility is constant for electrons and holes.

<img width="1305" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-40.png?raw=true"></br>

> Id = Vn(x) . Q(x) . W   -> (1)

In the above equation, substitute Vn(x) = 	μn . dV/dx </br>
Q(i) = -Cox([Vgs - V(x)]- Vt) </br>

Now, we will integrate the above equation (1),over the channel length (L), with the limits of dV will be from 0 to Vds and limits of dx will be from 0 to L (channel length). Thus get the simplest model for drain current (Id).</br>

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-41.png?raw=true"></br>


The simplest drain current equation that we get after simplification contains  Cox, W/L, Vgs, μn and Vt these are called as  <u>technology constants/technology parameters</u> or models for model file, these values are supplied to the  SPICE simulator to compute the value of drain current.</br>

<img width="" height="" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-42.png?raw=true"></br>

<img width="" height="" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-43.png?raw=true"></br>

<img width="" height="" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-44.png?raw=true"></br>

But, the above equation  is not a in Linear function,of voltage (Vds),from the equation, the drain current is a quadratic function of Vds. We will calculate the Id with the given values.

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-45.png?raw=true"></br>

From the above calculations we can conclude that if the value of (Vgs-Vt)>=Vds, the MOSFET operates in the <u>"Linear region /resistive region"</u> of operation.

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-46.png?raw=true"></br>

From the above calculation if the value of $Vds^2$ /2 value is less than 0,so its ignored.</br>

Now, the drain current (Id) becomes a linear function of Vds.
>Id =kn . (Vgs - Vt) Vds  ---> the MOSFET operates in the linear / resistive region of operation.

------

### <u>Lecture-4:-SPICE conclusion to resistive operation</u>

We need to find the impact of Vgs and Vds on the drain current equation.For this we will consider different values of Vgs and Vds. If we consider different values of Vgs, under what condition the device will remain in Linear/resistive region depends on (Vgs-Vt) value this should be greater than Vds.</br>

<img width="510" height="510" alt="image" src="https://github.com/Saikrupas/CMOS-Circuit-Design-SPICE-Simulation-SKY130-image-resources/blob/main/images-DAY1/img-47.png?raw=true"></br>

So, to calculate the value of Id for different values of 'Vgs', for every value of 'Vgs', we need to sweep Vds form 0 to (Vgs-Vt) to make the device operate in linear region of operation.</br>
For doing the calculations automatically we need to use SPICE simulations.</br>

-----





