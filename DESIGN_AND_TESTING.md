# 808 EQ+ — Design, Prototyping, and Testing

This document contains the detailed development process, circuit design, PCB design, enclosure design, additive-manufacturing information, and experimental results for the 808 EQ+ guitar pedal.

For the project overview, controls, build information, repository guide, and current release status, return to the [main README](README.md).

## Table of Contents

<details>
<summary><strong><a href="#design-and-prototyping-overview">Design and Prototyping Overview</a></strong></summary>

* [1. Circuit Research and Part-by-Part Analysis](#1-circuit-research-and-part-by-part-analysis)
* [2. Original TS808 Simulation and Breadboard Prototype](#2-original-ts808-simulation-and-breadboard-prototype)
* [3. Frequency-Response and Clipping Experiments](#3-frequency-response-and-clipping-experiments)
* [4. Perfboard, Faceless Enclosure, and Prototype Validation](#4-perfboard-faceless-enclosure-and-prototype-validation)
* [5. Component Selection and Price Optimization](#5-component-selection-and-price-optimization)
* [6. PCB Design in Altium Designer](#6-pcb-design-in-altium-designer)
* [7. Enclosure Remodeling and Mechanical Integration](#7-enclosure-remodeling-and-mechanical-integration)
* [8. Final Assembly and Testing](#8-final-assembly-and-testing)

</details>

<details>
<summary><strong><a href="#circuit-design">Circuit Design</a></strong></summary>

* [Signal-Path Overview](#signal-path-overview)
* [Power Supply and Bias Network](#power-supply-and-bias-network)
* [Input Buffer](#input-buffer)
* [Variable-Gain and Clipping Stage](#variable-gain-and-clipping-stage)
* [Active Tone Stage](#active-tone-stage)
* [Level Control and Output Buffer](#level-control-and-output-buffer)
* [True-Bypass and LED Circuit](#true-bypass-and-led-circuit)

</details>

<details>
<summary><strong><a href="#pcb-design">PCB Design</a></strong></summary>

* [Process Overview](#process-overview)
* [Design Priorities](#design-priorities)
* [Library Development](#library-development)
* [Through-Hole Components](#through-hole-components)
* [Socketed and Replaceable Components](#socketed-and-replaceable-components)
* [Routing and Grounding](#routing-and-grounding)
* [Manufacturer Selection and Design Files](#manufacturer-selection-and-design-files)

</details>

<details>
<summary><strong><a href="#enclosure-design-and-3d-printing">Enclosure Design and 3D Printing</a></strong></summary>

* [Why Use a Printed Enclosure?](#why-use-a-printed-enclosure)
* [Component-Driven Design](#component-driven-design)
* [Printed Labels and Graphics](#printed-labels-and-graphics)
* [Multi-Color Printing](#multi-color-printing)
* [Final Print Files and Recommended Settings](#final-print-files-and-recommended-settings)

</details>

<p><strong><a href="README.md">Return to the Main README</a></strong></p>

---

## Design and Prototyping Overview

The 808 EQ+ was developed through several stages, beginning with an in-depth study of the original TS808 circuit and progressing through simulation, breadboarding, measurement, perfboard prototyping, PCB design, enclosure modeling, and final assembly.

### 1. Circuit Research and Part-by-Part Analysis

The original TS808 circuit was studied in detail before beginning the physical design.

The [ElectroSmash](https://electrosmash.mas-effects.com/) Tube Screamer analysis was an especially useful reference. It provides an approachable but detailed explanation of the theory, mathematics, and behavior of the circuit and is a valuable resource for readers who want to understand why each stage operates as it does.

Additional background came from Sascha Suhr's book, [*Tracking Down Your Dream Tone — Build Your Own Guitar Effects Pedals: A Beginner's Guide*](https://www.amazon.com/dp/B09ZCJLB9J), which introduces both the theory and practical process involved in designing and building guitar effects pedals.

Other relevant concepts were researched through a wide range of freely available online educational resources. This research was supplemented by my background in computer engineering from the University of Utah.

Each major section of the TS808 circuit was analyzed separately, including:

* Input and output buffers
* Bias network
* Op-amp gain stage
* Frequency-dependent feedback
* Diode clipping
* Active tone control
* Power filtering
* Bypass behavior
* And other small intricacies

This research established a known working baseline and made it possible to evaluate later modifications without losing track of the original circuit behavior. The part-by-part analysis was also used to identify modern components that could replace less-available original parts while preserving their electrical function.

### 2. Original TS808 Simulation and Breadboard Prototype

The development process began with a publicly available schematic of the original [TS808 circuit](https://electrosmash.mas-effects.com/ElectroSmash%20-%20Tube%20Screamer%20Circuit%20Analysis.pdf). That unmodified circuit was first recreated in LTspice and then assembled on a breadboard using the original topology and modern, functionally equivalent components.

Establishing a working unmodified circuit *first* provided a reference against which every later change could be evaluated. Full-size potentiometers, audio jacks, and a DC barrel jack were integrated into the breadboard during this stage so the circuit could be evaluated as a complete pedal system.

The breadboard stage facilitated the analysis of:

* Basic signal flow
* Input and output buffer operation
* Bias voltages
* Drive, Tone, and Level control behavior
* Symmetric silicon clipping
* Practical operation with a guitar and amplifier

Images were not captured of the original unmodified LTspice circuit or breadboard prototype. However, images shown in the following section display the final circuit with the integrated EQ+ modifications.

### 3. Frequency-Response and Clipping Experiments

After the original circuit was operating correctly, the breadboard and LTspice models were modified one component and one circuit branch at a time.

The goal was to strike a useful balance between preserving the original TS808 character and adding meaningful tone-shaping options. The modifications were intended to be clearly audible without becoming either extreme or lackluster.

An Analog Discovery 2 and WaveForms software were used to examine:

* Frequency response
* Filter corner frequencies
* Gain changes
* Symmetric and asymmetric clipping
* Diode forward-voltage effects
* Output amplitude
* Waveform shape

Although these tools provided useful electrical measurements, a guitar-pedal circuit is difficult to characterize completely with a single set of tests. Its behavior can vary with the frequency and amplitude of the input signal, component tolerances, power-supply quality, radio-frequency interference, and other practical conditions. Each physical build may therefore behave slightly differently.

Final design decisions were made using a combination of circuit theory and analysis, LTspice simulation, Analog Discovery 2 measurements, and careful listening and experimentation with a guitar and amplifier. Measurements helped explain and compare circuit behavior, while hands-on playing determined whether each change was musically useful.

![Modified 808 EQ+ LTspice circuit](Images/Software/LTspice_Circuit.png)

*The circuit shown above is the final LTspice model containing the selected 808 EQ+ modifications.*

Much of the Bass Pass Through and Treble Pass Through development involved swapping capacitor and resistor values, adding new components, and testing those components at different points in the signal path. 

The final bass switch was implemented with a SPDT mechanical switch that swaps between C5 (default) and C12 (modified). The Bass Pass Through was designed to let enough low end through to give the guitar a thicker, fuller underbelly without making the distorted low frequencies excessively strong or muddy. The selected configuration lowers the distortion-stage high-pass corner from approximately **720 Hz to 410 Hz**.

The final treble switch was implemented with a SPDT mechanical switch that swaps between C7 (default) and C13 (modified). The Treble Pass Through was designed to give the pedal a significantly more transparent and open sound without making it excessively harsh or fizzy. The selected configuration raises the tone-stage low-pass corner from approximately **720 Hz to 3.4 kHz**.

The clipping-stage experiments compared several arrangements of LEDs and 1N4148 silicon diodes. These included symmetric and asymmetric configurations of each diode type, as well as arrangements that mixed LED and silicon diodes. The final configurations were selected because each provided a distinct and musically useful response.

The LEDs have a significantly higher forward voltage than the 1N4148 diodes. This raises the clipping threshold, producing substantially greater output volume, less compression, more headroom, and a more dynamic distortion response.

The asymmetric silicon configuration uses one 1N4148 diode in one direction and two series-connected 1N4148 diodes in the opposite direction. These branches are connected anti-parallel. It was selected as a subtle variation on the original TS808 configuration, which uses one 1N4148 diode in each direction. The asymmetric arrangement provides a slight increase in output volume and introduces additional even-order harmonic content, often associated with a thicker, more vintage-style sound.

*A photograph of the modified breadboard circuit will be added here.*

Several other possible features were also considered and tested, including:

* A switch for increased distortion
* A switch that changed the output resistor between TS808 and TS9 values
* A wet/dry blend control
* Additional diode configurations

These options were not included in the final design because their changes were underwhelming or insignificant, or because the additional circuitry and controls fell outside the intended scope and complexity of the project.

### 4. Perfboard, Faceless Enclosure, and Prototype Validation

After the breadboard design was stable, it was transferred to perfboard to create a compact, more permanent circuit that reduced loose wiring, established a practical layout, and could be mounted inside a pedal enclosure.

![Perfboard layout](Images/Software/Perfboard_DIYLayout.png)

The purpose of this design stage was to:

* Consolidate the circuit
* Integrate the true bypass foot switch
* Reduce breadboard-related connection problems
* Test the design in a more durable and portable pedal format
* Confirm the final circuit before beginning PCB design

The first 3D-printed enclosure prototype was developed in Autodesk Fusion 360 and focused primarily on fit and function rather than appearance. It provided a practical way to mount the circuit and controls before committing to the custom PCB and final enclosure design.

The perfboard + test enclosure prototype was used to confirm:

* Basic effect operation
* True bypass functionality
* Drive, Tone, and Level controls
* Bass and Treble Pass Through behavior
* Symmetric silicon clipping
* Asymmetric silicon clipping
* LED clipping
* Switch interaction
* Practical off-board wiring
* Overall sound and usability

This validation established the final circuit configuration that would then be transferred to a custom PCB.

The perfboard circuit and faceless enclosure also exposed practical problems that were not as apparent during breadboard testing. These steps were helpful in understanding the intricacies of developing an intuitive, visually appealing, and reliable pedal. They allowed me to refine the physical circuit-assembly process, develop a more compact and easy-to-use enclosure, and configure 3D-printing settings that balanced appearance, dimensional accuracy, and functionality.

*Photos of the perfboard circuit and faceless enclosure prototype will be added here.*

### 5. Component Selection and Price Optimization

Considerable time was spent selecting quality components for the later revisions. This work had to be completed before PCB design because the exact component dimensions, pin spacing, and package styles were required to create or verify footprints and plan the board layout.

Many parts used in the early breadboard and perfboard prototypes came from bulk component variety kits. For the custom PCB revision, the goal was to source only the required parts, reduce unnecessary purchases, improve component consistency, and streamline assembly.

Parts were compared through [Octopart](https://octopart.com/) and supplier catalogs from [DigiKey](https://www.digikey.com/), [LCSC](https://www.lcsc.com/), [Tayda Electronics](https://www.taydaelectronics.com/), [Mouser](https://www.mouser.com/en/), and other vendors. DigiKey was selected as the primary source for on-board electronic components because it offered all the required parts, reputable component quality, reasonable pricing, and the ability to consolidate the order through one supplier.

The available options from these suppliers were less suitable for much of the off-board hardware. [Love My Switches](https://lovemyswitches.com/) was selected for affordable, good-quality potentiometers and mono jacks. The SPDT toggle switches and true-bypass footswitches were purchased through Amazon because they were significantly less expensive and the parts had already proved reliable in the first prototype.

Each supplier was chosen by balancing component cost, quality, availability, and total shipping expense. Enough parts were purchased to build five pedals, which reduced the estimated per-pedal cost through quantity pricing and by spreading shipping costs across multiple builds.

All components used in the final design, along with part numbers, quantities, suppliers, and estimated pricing, are listed in the [`808_EQ-Plus_Single_Pedal_BOM.xlsx`](Design/808_EQ-Plus_Single_Pedal_BOM.xlsx) file in the repository’s `Design` folder.

### 6. PCB Design in Altium Designer

The validated circuit was redrawn and laid out in Altium Designer as a compact, reproducible through-hole PCB. The process converted the working prototype into a board that balanced enclosure fit, signal routing, hand-assembly accessibility, serviceability, and support for continued component experimentation.

This stage included building and verifying the component libraries, organizing the circuit into functional blocks, optimizing component placement and routing, preparing clear assembly markings, checking the completed design, comparing fabrication services, and generating the required manufacturing files.

For a complete discussion of the component libraries, construction choices, socketed parts, grounding, routing, manufacturer selection, and fabrication outputs, see [PCB Design](#pcb-design).

### 7. Enclosure Remodeling and Mechanical Integration

After the electronic design and PCB dimensions were better understood, the enclosure was remodeled in Fusion around the physical requirements of the circuit and off-board hardware. Simplified models of the PCB, controls, switches, jacks, power connector, LED, and related hardware were used to refine component spacing, openings, internal clearance, wire routing, assembly access, and the overall enclosure dimensions.

The resulting enclosure was designed specifically for 3D printing and incorporates the pedal’s mounting features, labels, graphics, custom knobs, LED holder, and removable bottom cover into a unified design.

For additional information about the modeling process, component placement, printed labels, materials, multi-color fabrication, tolerances, and print considerations, see [Enclosure Design and 3D Printing](#enclosure-design-and-3d-printing).

### 8. Final Assembly and Testing

The final phase began with assembling the manufactured PCB, inspecting the solder joints, and verifying the orientation of polarized components. The completed board was then tested outside the enclosure so that electrical or assembly problems could be identified and corrected before the off-board components were mounted.

After confirming basic PCB operation, the controls, switches, jacks, LED, and other off-board components were installed. Enclosure fit, bypass operation, effect operation, and every switch configuration were evaluated alongside the pedal’s drive, output level, tone, and overall usability. Any mechanical or electrical issues identified during this process were corrected through further revisions.

The enclosure-printing process was also refined in Bambu Studio to improve appearance, dimensional accuracy, component fit, and overall functionality. 

The completed PCB, enclosure, and assembled pedal have been fully tested and validated. Final fit checks confirmed that the PCB, off-board components, wiring, and printed enclosure function together as intended.

The final manufacturing files, PCB files, CAD exports, print files, dimensional drawings, and other supporting design resources have been released and are available in the repository’s [`Design`](Design/) folder.

---

## Circuit Design

The 808 EQ+ closely follows the original TS808 signal path while adding switchable filter and clipping options.

The detailed circuit explanation is still being developed. This section currently provides the organizational structure that will later be expanded with component references, equations, diagrams, and measurements.

### Signal-Path Overview

```text
Guitar In
  │
  ▼
Input Buffer
  │
  ▼
Variable-Gain and Clipping Stage
  │
  ▼
Active Tone and Treble-Filtering Stage
  │
  ▼
Level Control
  │
  ▼
Output Buffer
  │
  ▼
True-Bypass Footswitch
  │
  ▼
Effected Guitar Out
```

The circuit can be understood as a sequence of functional stages rather than as one large schematic.

![808 EQ+ schematic](Images/Software/Altium_Schematic.png)

### Power Supply and Bias Network

*To be expanded.*

This section will describe:

* 9 V center-negative power input
* Reverse-polarity protection
* Supply filtering
* Half-supply reference generation
* Decoupling
* Bias distribution throughout the signal path

### Input Buffer

*To be expanded.*

This section will describe:

* Input impedance
* Transistor-buffer operation
* Signal biasing
* Isolation of the guitar pickups from the clipping stage
* Similarities to the original TS808 input buffer

### Variable-Gain and Clipping Stage

*To be expanded.*

This section will describe:

* Non-inverting op-amp operation
* Drive-pot operation
* Minimum and maximum gain
* Frequency-dependent feedback
* Distortion-stage high-pass filtering
* Bass Pass Through switching
* Feedback-loop diode clipping
* Tight/Open switching
* Sym/Asym switching

The Bass Pass Through switch lowers the corner frequency of the distortion-stage high-pass filter from approximately **720 Hz to 410 Hz**.

The clipping network provides three configurations:

| Tight/Open | Sym/Asym        | Clipping configuration      | General character                                                                  |
| ---------- | --------------- | --------------------------- | ---------------------------------------------------------------------------------- |
| **Tight**  | **Sym**         | Symmetric silicon clipping  | Traditional TS808-style response with smooth compression and sustain.              |
| **Tight**  | **Asym**        | Asymmetric silicon clipping | Slightly greater output with additional grit and a less uniform clipping shape.    |
| **Open**   | Either position | Symmetric LED clipping      | Higher headroom, greater output, reduced compression, and a more dynamic response. |

### Active Tone Stage

*To be expanded.*

This section will describe:

* Original TS808 tone-control topology
* Lower-frequency and upper-frequency signal paths
* Active upper-frequency boost
* Tone-pot operation
* Tone-stage low-pass filtering
* Treble Pass Through switching

The Treble Pass Through switch raises the corner frequency of the tone-stage low-pass filter from approximately **720 Hz to 3.4 kHz**.

### Level Control and Output Buffer

*To be expanded.*

This section will describe:

* Level-pot placement
* Output-buffer operation
* Output coupling
* Output impedance
* Interaction with the true-bypass wiring

### True-Bypass and LED Circuit

*To be expanded.*

This section will describe:

* Mechanical signal routing
* Effect and bypass states
* Status LED switching
* LED current limiting
* Input and output jack connections

---

## PCB Design

The custom PCB was developed in Altium Designer to translate the validated prototype into a more durable, reproducible, and serviceable format.

### Process Overview

The PCB was developed through the following process:

1. Collect, revise, and organize the required schematic symbols and PCB footprints.
2. Redraw the complete schematic and assign the verified components, footprints, and designators.
3. Define the board shape and systematically place the through-hole components.
4. Position the off-board connection pads and orient component labels, values, and polarity markings for straightforward assembly.
5. Route the signal and power traces, then create the top and bottom ground pours.
6. Run electrical- and PCB-design-rule checks, correcting any identified problems.
7. Review the completed board in both 2D and 3D.
8. Generate the fabrication files and inspect the manufacturer previews before ordering.

| PCB top                                           | PCB bottom                                              |
| ------------------------------------------------- | ------------------------------------------------------- |
| ![PCB top](Images/Software/Altium_PCB_3D_Top.png) | ![PCB bottom](Images/Software/Altium_PCB_3D_Bottom.png) |

### Design Priorities

The PCB was designed around the following priorities:

* Preserve the validated TS808-style circuit
* Use readily solderable through-hole components
* Grouping components by functional circuit block
* Provide practical connection points for off-board wiring
* Support component replacement and experimentation
* Fit efficiently within the custom printed enclosure
* Minimize trace length, unnecessary crossings, and layer changes
* Provide clearly aligned component designators, value labels, and polarity markings
* Make fabrication possible through common prototype-PCB services

### Library Development

Many schematic symbols and PCB footprints were sourced from DigiKey and collected into organized Altium project libraries. Each resource was reviewed for dimensional accuracy and checked against the corresponding component datasheet to verify its pinout, package dimensions, and lead spacing. Existing library components were corrected when necessary, and custom symbols or footprints were created when suitable resources were unavailable.

The completed Altium library files are available in the repository’s [`Design/PCB/Altium`](Design/PCB/Altium/) folder.

### Through-Hole Components

Through-hole components were selected because they are relatively easy to solder by hand, inspect visually, and replace when necessary. They are also familiar to many hobbyists, readily available in small quantities, and compatible with machine-pin sockets for experimentation or repair. 

Although through-hole construction requires more board space than surface-mount construction, the increased accessibility and serviceability made the larger PCB area a worthwhile tradeoff.

### Socketed and Replaceable Components

Selected components can be installed in machine-pin sockets.

This is useful for:

* Comparing op-amps
* Comparing clipping diodes
* Replacing transistors
* Revising filter capacitors
* Troubleshooting damaged components
* Experimenting without repeatedly heating PCB pads

Sockets should be used selectively. Permanently installing every component in a socket would increase cost, assembly time, contact resistance, and the risk of intermittent connections.

Suggested components for machine-pin sockets include Q1, Q2, U1, C12, C13, and the clipping diodes. These locations are especially useful for tone experimentation, troubleshooting, repair, and comparing compatible replacement components.

### Routing and Grounding

The circuit’s typical current draw was measured at approximately **7–10 mA**. This range was entered into a PCB trace-width calculator, but the low current produced unusually narrow minimum-width recommendations. After researching trace widths commonly used by other guitar-pedal designers, wider traces were selected to provide more practical fabrication margins and greater physical robustness. The final layout uses **0.8 mm traces for the power rails** and **0.6 mm traces for signal paths**.

Signal traces were routed with attention to:

* Keeping related components close together
* Minimizing board area and trace length
* Reducing unnecessary trace crossings and layer changes
* Separating sensitive signal paths from power wiring
* Avoiding interference with through-hole pads
* Maintaining fabrication clearances

The board uses copper pours on both sides for ground distribution.

### Manufacturer Selection and Design Files

Several PCB manufacturers, including [OSH Park](https://oshpark.com/), [JLCPCB](https://jlcpcb.com/), [PCBWay](https://www.pcbway.com/orderonline.aspx), and [Elecrow](https://www.elecrow.com/pcb-manufacturing.html), were considered for producing the final board. Pricing, order quantities, fabrication options, shipping costs, turnaround time, and experiences reported by other hobbyists were compared. JLCPCB was ultimately selected because it offered an affordable option for the required boards and had received substantial positive feedback from other users online.

The relevant Altium project files, Gerber files, drill files, and other manufacturing outputs are available in the repository’s [`Design/PCB`](Design/PCB/) folder.

*Physical bare-PCB and assembled-PCB photographs will be added after final documentation is complete.*

---

## Enclosure Design and 3D Printing

The enclosure was designed as an integrated part of the project rather than as a generic box added after the electronics were complete.

![Bare enclosure](Images/Software/Fusion_Bare_Enclosure_Iso.png)

### Why Use a Printed Enclosure?

A printed enclosure provides several advantages:

* Lower cost than many commercial pedal enclosures
* Freedom over the outer shape and proportions
* Integrated labels and symbols
* Rapid revision of holes and component spacing
* Custom knobs and LED hardware
* Multiple colors without decals or screen printing
* Easy reproduction from digital files

The main tradeoffs are:

* Reduced impact resistance
* Reduced temperature resistance
* Reduced electromagnetic shielding
* Potentially longer fabrication time
* Greater dependence on print orientation and tolerances

> **Warning:** Common 3D-printing plastics may soften, warp, or deform at temperatures that would not damage a metal enclosure.

### Component-Driven Design

All enclosure-mounted components were modeled specifically for this project, including the potentiometers, toggle switches, footswitch, input and output jacks, DC power connector, PCB boundary, and LED. No existing component models were imported. Nuts, washers, and other fasteners were excluded because their detailed geometry was not necessary for the enclosure design.

These component models were used to determine the required hole diameters, internal spacing, PCB position, wire-routing space, footswitch clearance, jack depth, wall thickness, bottom-cover geometry, and tool access needed during assembly.

| Component placement                                               | Enclosure interior                                                      |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------- |
| ![Component placement](Images/Software/Fusion_Components_Top.png) | ![Enclosure interior](Images/Software/Fusion_Bare_Enclosure_Inside.png) |

The enclosure also includes:

* Custom printed knobs
* A custom LED holder
* Bottom-cover locating features
* Openings for enclosure-mounted components
* Print-aware wall thicknesses and tolerances
* A small access cutout that makes the bottom plate easier to remove after its screws have been removed

Dedicated PCB mounting features were intentionally omitted to simplify the enclosure design and final assembly process. Because the internal layout is compact, the PCB does not move freely once the pedal is fully assembled. The connected wiring constrains its position, while the bottom plate limits vertical movement and keeps the board mostly stationary inside the enclosure.

### Printed Labels and Graphics

The face labels and symbols are integrated into the enclosure model rather than applied afterward.

Contrasting filament is inlaid flush with the enclosure surface. The label geometry is designed to print against the build plate, producing a clean, flat front face without raised or recessed lettering.

A smooth PEI plate was used to improve the finish and readability of the labels. A textured plate may also work, but it can produce a shinier surface texture, less crisp lettering, more irregular edges, and blobbier or harder-to-read small text

### Multi-Color Printing

The current design uses **white filament** for most of the enclosure and selected accents on the knobs and LED holder. **Black filament** is used for the front-face inlays and as the primary color of the knobs and LED holder.

The Bambu H2S natively supports automatic multi-color printing, although each filament change produces additional purge waste. Because a single layer of black filament remained clearly visible against the white enclosure, the front-face inlays were intentionally made only one layer deep. This minimized the number of filament changes and reduced the amount of material wasted during purging.

The uploaded enclosure print files work best when the accent color is significantly darker than the primary enclosure color. Simply reversing the original color scheme would not produce an equivalent result. A single white inlay layer surrounded by black material would have poor opacity, appear closer to dark gray, and be much less visible than the black-on-white inlays.

Light or translucent accent colors should therefore be avoided when the primary enclosure color is dark. To use that type of color combination successfully, the inlay geometry should be modified to extend across additional layers, increasing its thickness and opacity. Other color combinations can be used without changing the enclosure’s overall mechanical design, provided that the contrast and opacity of the selected filaments are considered.

Multi-color fabrication is not strictly required. Possible alternatives include:

* Using recessed or raised labels and graphics
* Manually changing filament when printing
* Painting or filling the label geometry after printing
* Printing separate label inserts
* Omitting the cosmetic accents

| Sliced enclosure | Sliced underside |
| --- | --- |
| ![Sliced enclosure](Images/Software/BambuStudio_Enclosure_Sliced_Iso.png) | ![Sliced underside of enclosure](Images/Software/BambuStudio_Enclosure_Sliced_Underside.png) |

### Final Print Files and Recommended Settings

The enclosure design, print settings, tolerances, component fit, and appearance have been finalized and physically validated. The related files are available in the repository’s [`Design/3D_Printing`](Design/3D_Printing/) folder.

The provided file types serve different purposes:

* **STL files** contain the printable geometry for the enclosure and related parts. They can be imported into most slicers but do not preserve filament assignments, object placement, or slicer settings.
* **3MF files** contain prepared Bambu Studio projects with the models, object arrangement, filament assignments, and tested slicer settings. These files provide the best starting point for reproducing the validated prints on a compatible Bambu printer.

> [!CAUTION]
> The provided files and settings do not guarantee identical results on every printer. Dimensional accuracy, tolerances, surface finish, and label clarity can vary with the printer, filament, build plate, calibration, environmental conditions, and slicer version.
>
> The enclosure was designed around the specific off-board components listed in the project BOM. Substituting potentiometers, switches, jacks, connectors, fasteners, or other hardware may introduce dimensional differences that affect fit and assembly. Printed parts may require adjustment or reprinting, and the inlaid graphics and labels may not appear as clear as expected on every setup.
>
> The following settings produced the best results during development and may provide a useful starting point for further printer-specific tuning.

#### Importing, Positioning, and Model Preparation

When preparing the STL files manually:

1. Import the STL assembly containing the enclosure, inlays, and bottom plate.
2. Use **Lay on Face** to place the assembly on the enclosure’s top surface so the inlays contact the build plate.
3. Split the assembly into separate objects.
4. Move the bottom plate beside the enclosure.
5. Use **Lay on Face** to place the flat outer face of the bottom plate against the build plate.
6. Assign the appropriate filament to each object:
   * Assign filament 1 as the secondary accent color—black in the validated print.
   * Assign filament 2 as the primary enclosure color—white in the validated print.
   * In the **Objects** tab, assign the enclosure and bottom plate to the primary enclosure color.

#### Filament Printing Sequence

The accent inlays should print before the primary enclosure material:

1. Open the plate-specific customization settings.
2. Set **First layer filament sequence** to **Customize**.
3. Print the accent color first and the primary enclosure color second.
4. If the inlays extend beyond the first layer, configure **Other layer filament sequence** in the same order.

#### Modified Global Settings

| Setting | Validated value |
| --- | --- |
| Initial-layer line width | 0.42 mm |
| Seam position | Back |
| Elephant-foot compensation | 0.08 mm |
| Wall loops | 4 |
| Bottom shell layers | 4 |
| Internal solid infill pattern | Monotonic line |
| Sparse infill density | 25% |
| Sparse infill pattern | Cubic |
| Initial-layer speed | 25 mm/s |
| Support | Enabled |
| Support type | Normal (auto) |

#### Object-Specific Settings

For the enclosure and bottom plate:

* Enable **Only one wall on first layer**.
* Set **Bottom surface pattern** to **Monotonic Line**.

For the inlaid arrows and border:

* Set **Bottom surface pattern** to **Concentric**.
* Set **Seam position** to **Aligned**.

For the `9` object:

* Set **Seam position** to **Aligned**.

#### Seam Painting

Seam placement is particularly important around the bottom plate’s locating pegs and the corresponding slots in the enclosure. Poorly positioned seams can make these features larger or more irregular than intended and interfere with assembly.

* Paint the seam on each bottom-plate peg so it faces toward the center of the bottom plate.
* Verify that the corresponding peg slots in the enclosure do not contain seams that could interfere with insertion.
* If desired, align the enclosure’s outer seam with the bottom plate’s outer seam for a more consistent appearance.

---

Return to the [main project README](README.md).
