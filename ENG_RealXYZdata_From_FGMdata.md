# Table of Contents
<!-- MDTOC maxdepth:6 firsth1:0 numbering:1 flatten:0 bullets:1 updateOnSave:0 -->
- [Summary](#pSummary)

- [Synthesis and purposes](#pSynthesis)

- [1. Geomagnetic components in shortness](#p1)

    - [1.1 Usual procedure for obtaining continuous geomagnetic components](#p1_1)

    - [1.2 Discrete absolute measurements](#p1_2)

    - [1.3 Notes on building characteristics of flux-gate magnetometers](#p1_3)

        - [1.3.1 Mechanics of sensors system](#p1_3_1)

        - [1.3.2 Dynamic range of the sensors](#p1_3_2)

    - [1.4 Common interlude to the two types of sensor tern](#p1_4)

- [2. Essential flowchart of data processing in a geomagnetic observatory](#p2)

- [3. Variometric sensors on fixed tern, approach to the problem](#p3)

    - [3.1 Calculation of sensor rotation matrix applying least squares method](#p3_1)

    - [3.2 Estimate of residuals between the experimental values _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_,_Z<SUB>AID</SUB>_ and the values _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ rotated by sensor matrix](#p3_2)

    - [3.3 Estimate of the residuals interpolations and their addition to the _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ values rotated by the sensor matrix](#p3_3)

- [4. Variometric sensors arranged on cardanic suspension, approach to the problem](#p4)

    - [4.1 Calculation of rotation matrix for the _X<SUB>VAR</SUB>_ and _Y<SUB>VAR</SUB>_ components orthogonal to each other and lying in the horizontal plane, applying the least squares method](#p4_1)

    - [4.2 Estimate of residuals between the experimental values _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_ and the values _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ rotated by sensor matrix](#p4_2)

    - [4.3 Estimate of the residuals interpolations and their addition to the _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ values rotated by the sensor matrix](#p4_3)

    - [4.4 Calculation of continuous _Z<SUB>REA</SUB>_ values](#p4_4)

- [5. Linear systems gained](#p5)

- [6. Important notes about time](#p6)

    - [6.1 Time for sensors disposed on fixed tern](#p6_1)

        - [6.1.1 Calculation of sensor matrix - see (50), (51), (52) and residuals _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ - see (25)](#p6_1_1)

        - [6.1.2 Interpolation of the discrete series _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ in order to estimate the _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_, _Z<SUB>FitRES</SUB>_ continuous series - see (26)](#p6_1_2)

    - [6.2 Time for sensors disposed on cardanic suspension](#p6_2)

        - [6.2.1 Sensor matrix calculation - see (53), (54) and residuals _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ calculation - see (46)](#p6_2_1)

        - [6.2.2 Interpolation of the discrete series _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ in order to estimate the _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_ continuous series - see (47)](#p6_2_2)

- [7. Conclusions](#p7)

- [Acknowledgments](#pAcknowledgments)

- [Bibliography](#pBibliography)
<!-- /MDTOC -->

## Procedures to obtain *XYZ* cartesian geomagnetic components from flux-gate magnetometer measures (on Earth\'s observatories)

mr. Michele Di Savino, <michele.disavino@ingv.it>

<a name="pSummary"></a>
## Summary
The overall Earth\'s Magnetic Field, springs from the influence of multiple, non-separable, effects:<BR>ionosphere variations, own dipole magnetism, magnetic induction of the soil. It greatly conditions human life in frequently used civilian apparatuses and technologies; magnetic measurements are also carried out in non-invasive contexts such as medical diagnostics, environmental protection, energy and mining research, archeology, etc.<BR>
Ultimately, a number not at all small of human activities is influenced, directly or indirectly, by natural or artificial magnetic variations. Their monitoring therefore presents a certain importance; it is usually carried out by magnetometers located in sites with low electromagnetic noise level. They are detection tools that have followed the evolution of science and technology, becoming increasingly simple, stable, compact, precise and resolving. <BR>
This discussion is going to expose a data processing methodology supplied by a typical flux-gate sensors system, or in any case assimilable to it, aimed at calculating the fundamental geomagnetic elements in the cartesian reference trying to exploit to a greater extent the benefits deriving from an improved instrumentation.

<a name="pSynthesis"></a>
## Synthesis and purposes
The flux-gate magnetometer (later: FGM), generally provides vectorial measurements of the magnetic induction along three directions which are slightly different from the three geographical directions looked for: North-South, East-West and Vertical. <BR>
The following elaborations aim to obtain the correct magnetic components in the geographical reference. <BR>
Simultaneously, they implement a correction of the mechanical imbalance of the sensor system due to slow natural variations of the ground level or the occurrence of seismic events, of such intensity as to randomly shift the original position of the sensors. <BR><BR>
This report does not want to delve into peculiar aspects such as electronic excitation waveforms employed, sensor ferromagnetic characteristics, signal filters, adoption of technologies or components suitable for minimizing temperature effects, etcetera. <BR>
The FGM is considered in its most generic form; only two characteristics will be discussed in this report:
<BR> -Sensors positioned in fixed tern or tern provided of cardanic suspension; the two mathematical procedures are obviously different, even if conceptually identical.
<BR> -Dynamic range of the considered instrument. This is a transparent aspect for the elaborations to be performed, it managed by properly initializing three numerical variables: one for each recorded component *X*, *Y* and *Z*.

<a name="p1"></a>
## 1. Geomagnetic components in shortness
Next diagram shows the main elements used to describe the Earth\'s magnetic field: <BR>
<a name="Fig1"></a>
<BR> ![Figure 1](./Images/F1_AbsoluteTern.png) <BR>
**Figure 1.** Geomagnetic field elements

Considering a point _O<SUB>ABS</SUB>_ (*ABS*, i.e. absolute reference) on the Earth surface, the ![](./Images/Fabs_vec.png) magnetic induction vector passing through it, whatever it may be, can be decompose as a vector sum of three others: <BR>
![](./Images/Xabs_vec.png) directed along the geographical meridian, towards the North positive; <BR>
![](./Images/Yabs_vec.png) directed along the geographical parallel, towards the East positive; <BR>
![](./Images/Zabs_vec.png) directed along the vertical, downwards positive. <BR>

The result is the relation: ![](./Images/Fabs=Xabs,Yabs,Zabs_vecSum.png), while ![](./Images/Habs_vec.png) is the projection of ![](./Images/Fabs_vec.png) on the horizontal plane and therefore the following expressions also subsist:
![](./Images/Habs=Xabs,Yabs_vecSum.png) and ![](./Images/Fabs=Habs,Zabs_vecSum.png).

In addition, we define: <BR>
![](./Images/Dec.png) declination angle, is the angle between geographic north and magnetic north; it is positive if ![](./Images/Yabs_vec.png) is directed to East. <BR>
![](./Images/Inc.png) inclination angle, is the angle between horizontal plane and the ![](./Images/Fabs_vec.png) vector; it is positive if ![](./Images/Fabs_vec.png) is directed downwards. <BR>
![](./Images/Xabs_vec.png) , ![](./Images/Yabs_vec.png) and ![](./Images/Zabs_vec.png) form an orthogonal triplet of vectors oriented according to the geographic reference plus the vertical direction to the ground. <BR>

<a name="p1_1"></a>
## 1.1 Usual procedure for obtaining continuous geomagnetic components
The absolute components _X<SUB>ABS</SUB>, Y<SUB>ABS</SUB>, Z<SUB>ABS</SUB>_ play the fundamental role of reference measures.
The FGM provides continuous measurements of the geomagnetic field always in a three vector quantities likewise to the geographic reference, but in a different pseudo-random reference called variometric (later: *VAR*, variometric reference). <BR>
To return the continuous measurements made in the *VAR* reference into corresponding continuous and virtual values but in the *ABS* reference, the homologous *ABS*-*VAR* differences (i.e. baselines) are calculated at the time of absolute measurements. <BR>
These discrete differences are interpolated along the appropriate time interval and through mathematical inversion, the virtual *ABS* values are computed for all the time of the continuous readings in the *VAR* reference, for each of the three *XYZ* components. <BR>

<a name="p1_2"></a>
## 1.2 Discrete absolute measurements
The knowledge of the absolute geomagnetic components ![](./Images/Xabs_vec.png), ![](./Images/Yabs_vec.png) and ![](./Images/Zabs_vec.png) is generally achieved by measuring the magnetic angles ![](./Images/Dec.png) and ![](./Images/Inc.png) and knowing the value ![](./Images/Fabs_absolute.png) at corresponding time. <BR>
These measurements are manual and therefore discrete. <BR>

The magnetic angles ![](./Images/Dec.png) and ![](./Images/Inc.png) are found by rotating, by means of a demagnetized theodolite, along the horizontal and vertical circles, a magnetic field vector detector in search of the positions in which there is a value of the null field, (appliance named DIM, i.e. Declination Inclination Magnetometer), \[[Jankowski and Sucksdorff, 1996](#bIAGA)\]. <BR>

The aforementioned ![](./Images/Fabs_absolute.png) value is obtained from the measurement of a scalar magnetometer, usually a proton precession magnetometer or Overhauser effect magnetometer (later: SM scalar magnetometer), in permanently acquisition. <BR>

If necessary, the ![](./Images/Fabs_vec.png) module should be mathematically varied through a periodically verified constant, which takes into account the magnetic gradients between the various spots of the observatory where the measuring instruments are stood, see next [Figure 2](#Fig2). <BR>

<a name="p1_3"></a>
## 1.3 Notes on building characteristics of flux-gate magnetometers
Only two aspects of the used *VAR* instrument are taken into consideration here; according to these different characteristics, the mathematical procedures adopted vary. <BR>

<a name="p1_3_1"></a>
## 1.3.1 Mechanics of sensors system
The FGMs have terns of geomagnetic sensors with building characteristics of two main types: <BR>
fixed tern consisting of mutually orthogonal *X*,*Y*,*Z* sensors <BR>
and <BR>
tern composed of sensors arranged on a gimbal: the direction of *Z* sensor is always vertical by gravity while *X* and *Y* sensors, orthogonal to each other, are placed in a normal plane respect *Z* direction. <BR>

<a name="p1_3_2"></a>
## 1.3.2 Dynamic range of the sensors
The first FGM generations had a limited dynamic range, in fact each sensor worked artificially in a magnetic field around zero because otherwise the value of magnetic induction present would have easily saturated the sensor itself. <BR>
In this case the flux-gate sensors measured practically some variations, these last values went add to the main portions of magnetic component. <BR>
Each sensor core, was therefore equipped of electromagnetic compensation. <BR>
FGM characteristics of some IMO; (i.e. Intermagnet Magnetic Observatory). <BR>
DYNAMIC RANGE:  +/- 5000 nT (EBR, esp) <BR>
DYNAMIC RANGE:   +/- 500 nT (SPT, esp) <BR>
DYNAMIC RANGE:      6500 nT (LZH, chn) <BR>
\[[INTERMAGNET organization, 2014](#bIntermagnetDVD2010)\]. <BR>

The most advanced generations of FGM are designed with such a wide dynamic range as to exceed the measurable magnetic field induction value on the earth\'s surface. <BR>
In this event, the artificial electronic compensations of the three sensor cores are useless: <BR>
DYNAMIC RANGE:   Full field (all can) <BR>
DYNAMIC RANGE: +/- 80000 nT (all usa) <BR>
DYNAMIC RANGE: +/- 70000 nT (CLF, fra) <BR>
\[[INTERMAGNET organization, 2014](#bIntermagnetDVD2010)\]. <BR>

In the following, we will refer to *VAR* instruments with low dynamic range value, which therefore require an electronic compensation. <BR>
The treatment of the *VAR* instruments typology with a sufficiently high dynamic range is simpler, potentially more precise and it does not require formal changes to the procedures. <BR>
See next [§§3](#p3), [§§4](#p4). <BR>

<a name="p1_4"></a>
## 1.4 Common interlude to the two types of sensor tern

Taking into account the differences described in previous [§1.3.1](#p1_3_1) and [§1.3.2](#p1_3_2), fundamentally, resolutions can be implemented through variation of magnetic coordinates between the *VAR* reference (variometric and known) of departure, and the *ABS* reference (absolute and unknown) of arrival, for the homologous *XYZ* components.
<BR><BR> The solutions for tern equipped with fixed sensors and tern provided with sensors positioned on cardanic joint will be discussed, respectively, in [§§3](#p3) and [§§4](#p4).
<BR> The [§5](#p5) will present the full mathematical solutions for the two systems.
<BR> The [§§6](#p6) will argue the temporal conventions proposed for the resolution of the two types of sensors.
<BR> The last [§7](#p7) will compare the described methodology against the traditional procedure grounded on single baselines values reckoning.

<a name="p2"></a>
## 2. Essential flowchart of data processing in a geomagnetic observatory
The diagram highlights the different sites where the various instruments are positioned, they placed at a sufficient distance so as not to influence each other on the measurements taken.
<a name="Fig2"></a>
<BR> ![Figure 2](./Images/F2_Mag_flowchart.png) <BR>
**Figure 2.** Flowchart of geomagnetic data processing

The term ***static*** indicates numerical values, which under certain conditions, can be assumed constant. <BR>
The ***discrete*** wording signals discrete data. <BR>
The word ***continuous*** indicates continuous data. <BR>
The green box delimits the core of the particular procedures.

<a name="p3"></a>
## 3. Variometric sensors on fixed tern, approach to the problem
Recalling [Figure 1](#Fig1), we consider: <BR>
-number _N_ ordered triplets (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_) composed of magnetic induction values of the discrete absolute measurements obtained by DIM: this reference system originates in _O<SUB>ABS</SUB>_.

We define two magnetic points: <BR>
_O<SUB>VAR</SUB>_ is the origin of the variometric tern of continuous magnetic measurements; these last values are recorded by FGM, <BR>
_O<SUB>REA</SUB>_ is the origin of the tern of continuous virtual magnetic values that are calculated through the current procedure.

[Figure 3](#Fig3) shows the situation described:
<a name="Fig3"></a>
<BR> ![Figure 3](./Images/F3_Fix_Var.png) <BR>
**Figure 3.** Geomagnetic components read from the FGM variometer in its _O<SUB>VAR</SUB>_ reference (left), and transition to the real components in the _O<SUB>REA</SUB>_ reference (right)

The arrival origin is denominated _O<SUB>REA</SUB>_, but the components _X<SUB>REA</SUB>, Y<SUB>REA</SUB>, Z<SUB>REA</SUB>_ calculated at the end through the transformation are virtual and they refer to the origin _O<SUB>ABS</SUB>_, which is the observatory reference. <BR>
Thus, virtually, _O<SUB>REA</SUB>_ is equivalent to _O<SUB>ABS</SUB>_. <BR>

We consider also: <BR>
-ordered triplets (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) sampled at regular intervals by a set of three mutually orthogonal flux-gate sensors with unknown orientation. <BR>
The sensors ensemble is laid in the _O<SUB>VAR</SUB>_ point; this last is distinct from the _O<SUB>ABS</SUB>_ point. <BR>

-ordered triplet (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_). <BR>
Two cases must be separated according to the dynamic range characteristic of the *VAR* instrument used, see [§1.3.2](#p1_3_2). <BR>

High dynamic range. <BR>
In this case, it is sufficient to void the ordered triplet in question:
<BR> ![](./Images/eq1.png) <BR>
in all the subsequent formulas involved.

Low dynamic range. <BR>
Due to calculation mode that will be exposed starting from the next paragraph, it is necessary to estimate the values of the absolute *X*,*Y*,*Z* components in the _O<SUB>VAR</SUB>_ point at the moment when the orientation of the sensors ensemble happens.
<BR>
These values can be estimated quite easily through the execution of a concurrent absolute measurement, in fact it results:
<BR> ![](./Images/eq2.png) <BR>

where: <BR>
_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_ are the values obtained from the absolute measurement calculation,
<BR> ![](./Images/XYZgradients.png) represent the magnetic induction gradients between the *ABS* (i.e. DIM) and *VAR* (i.e. FGM) sites for the three components. <BR>
The ![](./Images/XYZgradients.png) gradients are nearly constant quantities, at least in the short term, and it is good practice to check them periodically. Undoubtedly more steady and small these quantities remain in time and better the quality of the geomagnetic observatory is. <BR>

Finally, at the same time, it is necessary to void electronically (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) on the *VAR* instrument, preferably in sync with the measurer on the DIM. <BR>

Once the sensor is set, if there are compensations (i.e. instrument with low dynamic range), the same adjustments must no longer be changed. <BR>

<a name="p3_1"></a>
## 3.1 Calculation of sensor rotation matrix applying least squares method
In this first phase, we consider the subset of _N_ ordered triplets (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) that matches to the time of the _N_ discrete absolute measurements (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_). <BR>

With contribution of the constant ordered triplet (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_), we can consider the usual mathematical expression that binds two generic orthogonal three-dimensional magnetic references:
<BR> ![](./Images/eq3.png) <BR>

where r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>,r<SUB>21</SUB>,r<SUB>22</SUB>,r<SUB>23</SUB>,r<SUB>31</SUB>,r<SUB>32</SUB>,r<SUB>33</SUB> are the nine elements of the _R<SUB>3x3</SUB>_ rotation matrix; they correlate the values read on the *VAR* site with the real values present on the *ABS* (or DIM) site. <BR>
For the calculation of this _R<SUB>3x3</SUB>_ matrix we only takes into account absolute measurements and variometer readings (*VAR* subscript), at discrete instants corresponding. <BR>
Such matrix is calculated with the contribution of the total signals of the FGM and, therefore, it takes into account also the undesired causes that can influence the long-term measurements: temperature drifts, electronic drifts and even mechanical leveling of the *VAR* instrument sensors ensemble. <BR>
By carrying out, we have:
<BR> ![](./Images/eq4.png) <BR>

to the first members of the three expressions, the following substitutions can be effectuated: <BR>
![](./Images/eq5,6,7.png) <BR>
*AID* subscript (i.e. *Abs Ini Difference*)

<a name="eq8"></a>
and the system becomes:
<BR> ![](./Images/eq8.png) <BR>

The three equations constituting (8) can be separated because the numerical values *AID* and *VAR* are known and imposed by extraction or calculation data. <BR>
We consider only the first equation included in (8):
<BR> ![](./Images/eq9.png) <BR>
and we examine the _N_ experimental values of the quantities reported.

The values of r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB> that best approximate the _N_ experimental values of _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_, _Z<SUB>VAR</SUB>_ bound by the relation (9) in the least squares sense, are obtained in the usual way by constructing the deviation:
<BR> ![](./Images/eq10.png) <BR>

and raising it to square:
<BR> ![](./Images/eq11.png) <BR>

The evolution _E_ of the square deviation, for the _N_ samples of _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_, _Z<SUB>VAR</SUB>_ is:
<BR> ![](./Images/eq12.png) <BR>

The minimum of _E(r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>)_ can be calculated by imposing the simultaneous annulment of the partial derivatives of _E_ in the variables r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>:
<BR> ![](./Images/eq13.png) <BR>

The satisfaction of this condition leads to the resolution of a linear system of rank 3 in which the unknowns are r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>13</SUB>. <BR>

First row of system:
<BR> ![](./Images/eq14,15.png) <BR>

i.e.
<BR> ![](./Images/eq16.png) <BR>

Second row of system:
<BR> ![](./Images/eq17,18.png) <BR>

i.e.
<BR> ![](./Images/eq19.png) <BR>

Third row of system:
<BR> ![](./Images/eq20,21.png) <BR>

i.e.
<BR> ![](./Images/eq22.png) <BR>

The six remaining elements r<SUB>21</SUB>,r<SUB>22</SUB>,r<SUB>23</SUB> and r<SUB>31</SUB>,r<SUB>32</SUB>,r<SUB>33</SUB> of the rotation matrix are obtained by two analogous procedures applying the right experimental data series to the equations:
<BR> ![](./Images/eq23.png) <BR>
and
<BR> ![](./Images/eq24.png) <BR>
of the system [\(8\)](#eq8).

<a name="p3_2"></a>
## 3.2 Estimate of residuals between the experimental values _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_,_Z<SUB>AID</SUB>_ and the values _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ rotated by sensor matrix
The information achieved through the compute of the _R<SUB>3x3</SUB>_ rotation matrix will be subsequently integrated using residuals between the experimental absolute values (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_) and the values (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) detected by the variometer and afterwards rotated, at the time of absolute measurements performed. <BR>
These discrete residuals, for each of the _N_ points, are calculated as following: <BR>
<a name="eq25"></a> <BR>
![](./Images/eq25.png) <BR>

<a name="p3_3"></a>
## 3.3 Estimate of the residuals interpolations and their addition to the _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_,_Z<SUB>VAR</SUB>_ values rotated by the sensor matrix
Interpolating these _N_ ordinated triplets of discrete residuals (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) calculated from (25) with their appropriate independent time variables, for the whole interval time involved, we obtain the continuous ordinated triplets (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>,Z<SUB>FitRES</SUB>_) that provide the optimal corrections to be add to the contribution of the continuous values (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) multiplied for the rotation matrix of the sensor: <BR>
<a name="eq26"></a> <BR>
![](./Images/eq26.png) <BR>

The real values (_X<SUB>REA</SUB>,Y<SUB>REA</SUB>,Z<SUB>REA</SUB>_) calculated are relative to the *ABS* (or DIM) site, but they obtained physically from the corresponding numerical values (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) continuously recorded by the flux-gate *VAR* instrument with random orientation.

Due to the execution of absolute measurements through DIM and the mathematical techniques adopted, the practical implementation of the methods exposed requires considerations on the time of both the absolute measurements performed *XYZF AID* and the data considered *XYZF VAR*: one of these possibilities will be presented in the last [§§6](#p6). <BR>
Until debate these paragraphs, the procedures developed will not take into account of precise time.

<a name="p4"></a>
## 4. Variometric sensors arranged on cardanic suspension, approach to the problem
Recalling [Figure 1](#Fig1), we consider: <BR>
-number _N_ ordered pairs (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>_) and _Z<SUB>ABS</SUB>_ quantities composed of magnetic induction values of the discrete absolute measurements obtained by DIM: this reference system originates in _O<SUB>ABS</SUB>_.

We define two magnetic points: <BR>
_O<SUB>VAR</SUB>_ is the origin of the variometric tern of continuous magnetic measurements; these last values are recorded by FGM, <BR>
_O<SUB>REA</SUB>_ is the origin of the tern of the continuous virtual magnetic measurements that are calculated through the current procedure.

[Figure 4](#Fig4) shows the situation described:
<a name="Fig4"></a>
<BR> ![Figure 4](Images/F4_Gimbal_Var.png) <BR>
**Figure 4.** Geomagnetic components read from the FGM variometer in its _O<SUB>VAR</SUB>_ reference (left), and transition to the real components in the _O<SUB>REA</SUB>_ reference (right)

The arrival origin is denominated _O<SUB>REA</SUB>_, but the components _X<SUB>REA</SUB>, Y<SUB>REA</SUB>, Z<SUB>REA</SUB>_ calculated at the end through the transformation are virtual and they refer to the origin _O<SUB>ABS</SUB>_, which is the observatory reference. <BR>
Thus, virtually, _O<SUB>REA</SUB>_ is equivalent to _O<SUB>ABS</SUB>_. <BR>

We consider also: <BR>
-ordered pairs (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) and _Z<SUB>VAR</SUB>_ quantities sampled at regular intervals by a set of three flux-gate vectorial sensors arranged on a cardanic joint. <BR>
The sensors ensemble is laid in the _O<SUB>VAR</SUB>_ point; this last is distinct from the _O<SUB>ABS</SUB>_ point. <BR>

The sensors tern which measure (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) and _Z<SUB>VAR</SUB>_ is suspended and the vertical along the direction of the weight force and the sensitive direction of the _Z<SUB>VAR</SUB>_ component coincide, so _Z<SUB>VAR</SUB>_ really measures a quantity proportional to the real vertical component _Z<SUB>REA</SUB>_. <BR>
Based on the mechanical construction of the sensors ensemble, the other two sensitive directions _X<SUB>VAR</SUB>_ and _Y<SUB>VAR</SUB>_ of the flux-gate tern are orthogonal to each other and both orthogonal to the sensitive direction of the _Z<SUB>VAR</SUB>_ component. <BR>
Although the sensitive direction of the _Z<SUB>VAR</SUB>_ component is always vertical, the horizontal plane can rotate around the vertical axis and therefore the directions of the _X<SUB>VAR</SUB>_ and _Y<SUB>VAR</SUB>_ components are not immutable. <BR>

-ordered triplet (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_). <BR>
Two cases must be separated according to the dynamic range characteristic of the *VAR* instrument used, see [§1.3.2](#p1_3_2). <BR>

High dynamic range. <BR>
In this case, it is sufficient to void the ordered triplet in question:
<BR> ![](./Images/eq27.png) <BR>
in all the subsequent formulas involved.

Low dynamic range. <BR>
Due to calculation mode that will be exposed starting in the next paragraph, it is necessary to estimate the values of the absolute *X*,*Y*,*Z* components in the _O<SUB>VAR</SUB>_ point at the moment when the orientation of the sensors ensemble happens.
<BR>
These values can be estimated quite easily through the execution of a concurrent absolute measurement, in fact it results:
<BR> ![](./Images/eq28.png) <BR>

where: <BR>
_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>,Z<SUB>ABS</SUB>_ are the values obtained from the absolute measurement calculation,
<BR> ![](./Images/XYZgradients.png) represent the magnetic induction gradients between the *ABS* (i.e. DIM) and *VAR* (i.e. FGM) sites for the three components. <BR>
The ![](./Images/XYZgradients.png) gradients are nearly constant quantities, at least in the short term, and it is good practice to check them periodically. Undoubtedly more steady and small these quantities remain in time and better the quality of the geomagnetic observatory is. <BR>

Finally, at the same time, it is necessary to void electronically (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) on the *VAR* instrument, preferably in sync with the measurer on the DIM. <BR>

Once the sensor is set, if there are compensations (i.e. instrument with low dynamic range), the same adjustments must no longer be changed. <BR>

The presence of the cardan joint allows to separate the elaborations for the (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) ordered pairs, see [§4.1](#p4_1), [§4.2](#p4_2) e [§4.3](#p4_3); from the elaborations concerning the _Z<SUB>VAR</SUB>_ components, see [§4.4](#p4_4). <BR>

<a name="p4_1"></a>
## 4.1 Calculation of rotation matrix for the _X<SUB>VAR</SUB>_ and _Y<SUB>VAR</SUB>_ components orthogonal to each other and lying in the horizontal plane, applying the least squares method
Unlike the fixed tern sensor, the elaboration for _X<SUB>AID</SUB>_, _Y<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_ is completely separate from the one concerning _Z<SUB>AID</SUB>_, _Z<SUB>VAR</SUB>_. <BR><BR>
In this first phase, we consider the subset of _N_ ordered pairs (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) that matches to the time of the _N_ discrete absolute measurements (_X<SUB>ABS</SUB>,Y<SUB>ABS</SUB>_). <BR>

With contribution of the constant ordered pair (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>_), we can consider the usual mathematical expression that binds two generic orthogonal bi-dimensional magnetic references:
<BR> ![](./Images/eq29.png) <BR>

where r<SUB>11</SUB>,r<SUB>12</SUB>,r<SUB>21</SUB>,r<SUB>22</SUB> are the four elements of the _R<SUB>2x2</SUB>_ rotation matrix; they correlate the values read on the *VAR* site with the real values present on the *ABS* (or DIM) site. <BR>
For the calculation of this _R<SUB>2x2</SUB>_ matrix we only takes into account absolute measurements and variometer readings (*VAR* subscript), at discrete instants corresponding. <BR>
Such matrix is calculated with the contribution of the total signals of the FGM and, therefore, it takes into account also the undesired causes that can influence the long-term measurements: temperature drifts, electronic drifts and even mechanical leveling of the *VAR* instrument sensors ensemble. <BR>
By carrying out, we have:
<BR> ![](./Images/eq30.png) <BR>

to the first members of the two expressions, the following substitutions can be effectuated: <BR>
![](./Images/eq31,32.png) <BR>
*AID* subscript (i.e. *Abs Ini Difference*)

<a name="eq33"></a>
and the system becomes:
<BR> ![](./Images/eq33.png) <BR>

The two equations constituting (33) can be separated because the numerical values *AID* and *VAR* are known and imposed by extraction or calculation data. <BR>
We consider only the first equation included in (33): <BR>
![](./Images/eq34.png) <BR>
and we examine the _N_ experimental values of the quantities reported.

The values of r<SUB>11</SUB>,r<SUB>12</SUB> that best approximate the _N_ experimental values of _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_ bound by the relation (34) in the least squares sense, are obtained in the usual way by constructing the deviation:
<BR> ![](./Images/eq35.png) <BR>

and raising it to square:
<BR> ![](./Images/eq36.png) <BR>

The evolution _E_ of the square deviation, for the _N_ samples of _X<SUB>AID</SUB>_, _X<SUB>VAR</SUB>_, _Y<SUB>VAR</SUB>_ is:
<BR> ![](./Images/eq37.png) <BR>

The minimum of _E(r<SUB>11</SUB>,r<SUB>12</SUB>)_ can be calculated by imposing the simultaneous annulment of the partial derivatives of _E_ in the variables r<SUB>11</SUB>,r<SUB>12</SUB>:
<BR> ![](./Images/eq38.png) <BR>

The satisfaction of this condition leads to the resolution of a linear system of rank 2 in which the unknowns are r<SUB>11</SUB>,r<SUB>12</SUB>. <BR>

First row of sistem:
<BR> ![](./Images/eq39,40.png) <BR>

i.e.
<BR> ![](./Images/eq41.png) <BR>

Second row of sistem:
<BR> ![](./Images/eq42,43.png) <BR>

i.e.
<BR> ![](./Images/eq44.png) <BR>

The two remaining elements r<SUB>21</SUB>,r<SUB>22</SUB> of the rotation matrix are obtained by analogous procedure applying the right experimental data series to the equation:
<BR> ![](./Images/eq45.png) <BR>
of the system [\(33\)](#eq33).

<a name="p4_2"></a>
## 4.2 Estimate of residuals between the experimental values _X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_ and the values _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ rotated by sensor matrix
The information achieved through the compute of the _R<SUB>2x2</SUB>_ rotation matrix, will be subsequently integrated using residuals between the experimental absolute values (_X<SUB>AID</SUB>_,_Y<SUB>AID</SUB>_) and the values (_X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_) detected by the variometer and afterwards rotated, at the time of absolute measurements performed. <BR>
These discrete residuals, for each of the _N_ points, are calculated as following: <BR>
<a name="eq46"></a> <BR>
![](./Images/eq46.png) <BR>

<a name="p4_3"></a>
## 4.3 Estimate of the residuals interpolations and their addition to the _X<SUB>VAR</SUB>_,_Y<SUB>VAR</SUB>_ values rotated by the sensor matrix
Interpolating these _N_ ordinated pairs of discrete residuals (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) calculated from (46) with their appropriate independent time variables, for the whole interval time involved, we obtain the continuous ordinated pairs (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>_) that provide the optimal corrections to be add to the contribution of the continuous values (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) multiplied for the rotation matrix of the sensor: <BR>
<a name="eq47"></a> <BR>
![](./Images/eq47.png) <BR>

The real values (_X<SUB>REA</SUB>,Y<SUB>REA</SUB>_) calculated are relative to the *ABS* (or DIM) site, but they obtained physically from the corresponding numerical values (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) continuously recorded by the flux-gate *VAR* instrument with random orientation.

Due to the execution of absolute measurements through DIM and the mathematical techniques adopted, the practical implementation of the methods exposed requires considerations on the time of both the absolute measurements performed *XYZF AID* and the data considered *XYZF VAR*: one of these possibilities will be presented in the last [§§6](#p6). <BR>
Until debate these paragraphs, the procedures developed will not take into account of precise time.

<a name="p4_4"></a>
## 4.4 Calculation of continuous _Z<SUB>REA</SUB>_ values
The sensitive element of the vector component _Z<SUB>VAR</SUB>_ always assumes a vertical orientation due to the mechanical construction of the sensor tern, therefore for each value of the continuous sampling _Z<SUB>VAR</SUB>_, the corresponding continuous value _Z<SUB>REA</SUB>_ immediately descends:
<BR> ![](./Images/eq48.png) <BR>

Where the continuous values _Z<SUB>FitBAS</SUB>_ are obtained preliminarily by the interpolation of the baseline terms _Z<SUB>BAS</SUB>_ of discrete absolute measurements and calculated individually as:
<BR> ![](./Images/eq49.png) <BR>

In the building of continuous series _Z<SUB>FitBAS</SUB>_, it has been chosen to repeat the only _Z<SUB>BAS</SUB>_ value computed for each single minute concerning the inclination measurement. <BR>
These interpolations have independent variables represented by right inclination measure time. <BR>

Instead, to evaluate the discrete value of (49), _Z<SUB>ABS</SUB>_ (i.e. _Z<SUB>AID</SUB>_) is the only calculated value, while _Z<SUB>VAR</SUB>_ is obtained by computing the average between all the values of _Z<SUB>VAR</SUB>_ registered at the inclination time of the absolute measure considered.

<a name="p5"></a>
## 5. Linear systems gained
Linear systems for calculating matrices of rotation, for both types of *VAR* sensor, are shown for completeness below:

sensors on fixed tern:
<a name="eq50"></a> <BR>
![](./Images/eq50.png) <BR>

<a name="eq51"></a> <BR>
![](./Images/eq51.png) <BR>

<a name="eq52"></a> <BR>
![](./Images/eq52.png) <BR>

sensors on gimbal:
<a name="eq53"></a> <BR>
![](./Images/eq53.png) <BR>

<a name="eq54"></a> <BR>
![](./Images/eq54.png) <BR>

Like we can verify, in the linear systems of order 3 (or 2), the incomplete matrices remain constant, instead the matrices of known terms varies, depending on the rows of the rotation matrix to calculate.

<a name="p6"></a>
## 6. Important notes about time
The next diagram focalizes the time of a typical absolute measure (from [Figure 1](#Fig1)\):
<a name="Fig5"></a>
<BR> ![Figure 5](./Images/F5_AbsoluteMeasureView.PNG) <BR>
**Figure 5.** Time of execution DIM measure <BR>
<BR> \[[Jankowski and Sucksdorff, 1996](#bIAGA)\]. <BR>
For a correct application of the methodologies, for each absolute measure, all the components must be present:
<BR> Both ordered triplets (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_) and (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_), for sensors on fixed tern.
<BR> Both ordered pairs (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>_) and (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_), for tern equipped with tilting suspension.
<BR> This can be verified by looking at the available data.

Each absolute measure considered should be executed in an instant; this does not usually occur, in fact for an absolute measure, the declination and inclination readings can take more minutes. <BR>
Follow some proposals for to implement time in procedures.

<a name="p6_1"></a>
## 6.1 Time for sensors disposed on fixed tern
<a name="p6_1_1"></a>
## 6.1.1 Calculation of sensor matrix - see [\(50\)](#eq50), [\(51\)](#eq51), [\(52\)](#eq52) and residuals _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ - see [\(25\)](#eq25)

In the computation of these elements take part the _N_ ordered triplets (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_) and (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_), considered at the time of the discrete absolute measurements. <BR>
Both the rotation matrix _R<SUB>3x3</SUB>_ and the ordered discrete triplets (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) achieved, derive from the least squares calculation and they are not concerning to specific time. <BR>

The values that compose (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>,Z<SUB>AID</SUB>_), as seen in [Figure 5](#Fig5) above, are certainly measured in not negligible time intervals but, considering that in the calculation of the least squares the values of time are irrelevant, we simply assume each absolute measurement as a single entity. <BR>

The (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>,Z<SUB>VAR</SUB>_) values instead can be chosen among all those continuously measured by the *VAR* instrument, at the time involved in the absolute measurement, namely: <BR>
Calculation of the average among all the _X<SUB>VAR</SUB>_ (or _Y<SUB>VAR</SUB>_) values acquired in the time of declination measure, together with those acquired in the time of inclination measure. <BR>
Calculation of the average among all the _Z<SUB>VAR</SUB>_ values acquired in the time of inclination measure. <BR>

<a name="p6_1_2"></a>
## 6.1.2 Interpolation of the discrete series _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_, _Z<SUB>RES</SUB>_ in order to estimate the _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_, _Z<SUB>FitRES</SUB>_ continuous series - see [\(26\)](#eq26)
The _N_ discrete ordered triplets (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) take part in the calculation of these interpolations, with independent variables the time of the absolute measurements. <BR>
As reported in the previous [§6.1.1](#p6_1_1), also the ordered triples (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) are considered like entities dependent on the determined absolute measure, but without associated time. <BR>

The continuous ordered triplets (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>,Z<SUB>FitRES</SUB>_) are obtained by interpolating, through the chosen method, the discrete ordered triplets (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>,Z<SUB>RES</SUB>_) considering the appropriate time intervals. <BR>
To this end, specific time have been reintroduced coherently with the logical paths shown in [Figure 5](#Fig5): <BR>
To calculate the _X<SUB>FitRES</SUB>_ (or _Y<SUB>FitRES</SUB>_) series, the _X<SUB>RES</SUB>_ (or _Y<SUB>RES</SUB>_) values have been interpolated with independent variables the declination time joined with the inclination time, of the particular absolute measurement. <BR>
To calculate the _Z<SUB>FitRES</SUB>_ series, the _Z<SUB>RES</SUB>_ values have been interpolated with independent variables the inclination time of the particular absolute measurement. <BR>

Moreover: <BR>
The same value of _X<SUB>RES</SUB>_ (or _Y<SUB>RES</SUB>_) associated with the absolute measure considered, has been repeated for every single minute that constitutes the time interval of the declination and inclination. <BR>
With similar policy, the _Z<SUB>RES</SUB>_ value associated with the absolute measure considered, has been repeated for every single minute that constitutes the time interval of the inclination.

<a name="p6_2"></a>
## 6.2 Time for sensors disposed on cardanic suspension
<a name="p6_2_1"></a>
## 6.2.1 Sensor matrix calculation - see [\(53\)](#eq53), [\(54\)](#eq54) and residuals _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ calculation - see [\(46\)](#eq46)
In the computation of these elements take part the _N_ ordered pairs (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>_) and (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_), considered at the time of the discrete absolute measurements.
<BR> Both the _R<SUB>2x2</SUB>_ rotation matrix  and the ordered discrete pairs (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_), derive from the least squares calculation and they are not concerning to specific time.

The values that compose (_X<SUB>AID</SUB>,Y<SUB>AID</SUB>_), as seen in [Figure 5](#Fig5) above, are certainly measured in not negligible time intervals but, considering that in the calculation of the least squares the values of time are irrelevant, we simply assume each absolute measurement as a single entity.

The (_X<SUB>VAR</SUB>,Y<SUB>VAR</SUB>_) values instead can be chosen among all those continuously measured by the *VAR* instrument, at the time involved in the absolute measurement, namely: <BR>
Calculation of the average among all _X<SUB>VAR</SUB>_ (or _Y<SUB>VAR</SUB>_) values acquired in the time of declination measure, together with those acquired in the time of inclination measure.

<a name="p6_2_2"></a>
## 6.2.2 Interpolation of the discrete series _X<SUB>RES</SUB>_, _Y<SUB>RES</SUB>_ in order to estimate the _X<SUB>FitRES</SUB>_, _Y<SUB>FitRES</SUB>_ continuous series - see [\(47\)](#eq47)
The _N_ discrete ordered pairs (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) take part in the calculation of these interpolations, with independent variables the time of the absolute measurements. <BR>
As reported in the previous [§6.2.1](#p6_2_1), also the ordered pairs (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) are considered like entities dependent on the determined absolute measure, but without associated time. <BR>

The continuous ordered pairs (_X<SUB>FitRES</SUB>,Y<SUB>FitRES</SUB>_) are obtained by interpolating, through the chosen method, the discrete ordered pairs (_X<SUB>RES</SUB>,Y<SUB>RES</SUB>_) considering the appropriate time intervals. <BR>
To this end, specific time have been reintroduced coherently with the logical paths shown in [Figure 5](#Fig5): <BR>
To calculate the _X<SUB>FitRES</SUB>_ (or _Y<SUB>FitRES</SUB>_) series, the _X<SUB>RES</SUB>_ (or _Y<SUB>RES</SUB>_) values have been interpolated with independent variables the declination time joined with the inclination time, of the particular absolute measurement. <BR>

Moreover: <BR>
The same value of _X<SUB>RES</SUB>_ (or _Y<SUB>RES</SUB>_) associated with the absolute measure considered, has been repeated for every single minute that constitutes the time interval of the declination and inclination.

<a name="p7"></a>
## 7. Conclusions
These conversion methods can be used indifferently for FGM sensors terns laid both on *HDZ* and *XYZ* orientation \[[Technical University of Denmark, 2014](#bDTU_Orie)\] or rather, like discussed, theoretically the orientation of the sensors system can be random. <BR>

Logically, it is useful to regularly place the sensors ensemble in the *HDZ* or *XYZ* orientation and then combine both procedures:  <BR>
-Initially the one with traditional reduction formulas and calculation of single baseline values for a preliminary verification of the baselines: general control of the acquisition, electronic and temperature drifts or to build provisional data \[[Rigler, 2015](#bUSGS_Red); [DANISH METEOROLOGICAL INSTITUTE, TECHNICAL REPORT 04-14, 2004](#bDMI_Red)\]. <BR>
-Later, when all the data series will be available, it will be convenient to apply the described techniques with the use of least squares and residuals. This operation also compensate for the ground leveling and the definitive data are constructed. <BR>

In the presence of known or random displacements due to earthquakes interesting the sensor tern, it is obviously advisable to perform absolute measurements as soon as possible after the event that has changed the position of the sensor system.  <BR>
If it result convenient, the data series can be appropriately split to increase the accuracy of the partial results. <BR>
In the presence of FGM having low dynamic range values, it is generally not necessary to proceed with a new acquisition of initial values (_X<SUB>INI</SUB>,Y<SUB>INI</SUB>,Z<SUB>INI</SUB>_). <BR>
In fact, even if the position of the sensor tern is formally changed, if the laying site has a low magnetic gradient, the initial conditions are almost unaltered: the necessary precaution remains that of not modifying the initial electronic adjustments. <BR>

Using the traditional reduction formulas, see [§1.1](#p1_1), a single numerical interpolation is performed on the baseline values (for each magnetic component); while with the method exposed the estimation is performed twice: <BR>
\- the first one calculates the fixed rotation matrix: see [§3.1](#p3_1) for _R<SUB>3x3</SUB>_ or  [§4.1](#p4_1) for _R<SUB>2x2</SUB>_. <BR>
\- the second one calculates the interpolation of the residuals to compensate the values produced by the rotation carried out by means the fixed matrix of the sensor: see [§3.3](#p3_3) for _R<SUB>3x3</SUB>_ or [§4.3](#p4_3) for _R<SUB>2x2</SUB>_. <BR>

Evidently, this leads to an increase in computational error. On the other hand, these procedures are particularly suitable for FGM sensors installed in places characterized by a certain seismicity or subject to appreciable slow natural variations of ground level because they are based on \"true\" real values.
<BR> For example, they allow to minimize the consequences of a random displacement of sensors ensemble on horseback an important seismic event.

<a name="pAcknowledgments"></a>
## Acknowledgments
The results presented in this paper rely on data collected at magnetic observatories. We thank the national institutes that support them and INTERMAGNET for promoting high standards of magnetic observatory practice ([www.intermagnet.org](http://www.intermagnet.org)).

<a name="pBibliography"></a>
## Bibliography

<a name="bDMI_Red"></a>
DANISH METEOROLOGICAL INSTITUTE, TECHNICAL REPORT 04-14, (2004). *Magnetic Results 2003 Brorfelde, Qeqertarsuaq, Qaanaaq and Narsarsuaq Observatories.* DANISH METEOROLOGICAL INSTITUTE, Copenhagen, pp. 5. <BR>
web page: <https://www.intermagnet.org/yearbooks/Denmark_2003.pdf>

Hitchman A.P., Crosthwaite P.G., Jones W.V., Lewis A.M., Wang L., (2011). *Australian Geomagnetism Report 2010, Volume 58*. Geoscience Australia, pp. 3. <BR>
web page: <https://www.intermagnet.org/yearbooks/Australia_2010.pdf>

INTERMAGNET organization, (2012). *INTERMAGNET Technical Reference Manual Version 4.6.* <BR>
web page: <https://www.intermagnet.org/publications/intermag_4-6.pdf>

<a name="bIntermagnetDVD2010"></a>
INTERMAGNET organization, (2014). *MAGNETIC OBSERVATORY DEFINITE DATA, INTERMAGNET 2010,* Observatory Information, DVD ROM.

<a name="bIAGA"></a>
Jankowski J. and Sucksdorff C., (1996). *GUIDE FOR MAGNETIC MEASUREMENTS AND OBSERVATORY PRACTICE*. IAGA organization, Warsaw, pp. 15-16, 87-98. <BR>
web page: <http://www.iaga-aiga.org/data/uploads/pdf/guides/iaga-guide-observatories.pdf>

<a name="bUSGS_Red"></a>
Rigler E. J., (2015). *XYZ Algorithm.* U.S. Geological Survey. <BR>
github page: <https://github.com/usgs/geomag-algorithms/blob/master/docs/algorithms/XYZ.md>

<a name="bDTU_Orie"></a>
Technical University of Denmark, (2014). *FLUXGATE MAGNETOMETER Suspended version Model FGE version K2 Manual.* DTU Space, National Space Institute, pp. 12-13. <BR>
web page: <https://www.space.dtu.dk/english/-/media/Institutter/Space/English/instruments_systems_methods/3-axis_fluxgate_magnetometer_model_fgm-fge/FGEFluxgateMagnetometerManual.ashx>
<BR>
^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>^<BR>
