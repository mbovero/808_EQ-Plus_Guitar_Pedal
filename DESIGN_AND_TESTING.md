# 808 EQ+ — Design, Prototyping, and Testing

This document contains the detailed development process, circuit design, PCB design, enclosure design, additive-manufacturing information, and experimental results for the 808 EQ+ guitar pedal.

For the project overview, controls, build information, repository guide, and current release status, return to the [main README](README.md).

## Table of Contents

<details>
<summary><strong><a href="#design-and-prototyping-process">Design and Prototyping Process</a></strong></summary>

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

* [Design Priorities](#design-priorities)
* [Library Development](#library-development)
* [Through-Hole Construction](#through-hole-construction)
* [Socketed and Replaceable Components](#socketed-and-replaceable-components)
* [Grounding and Routing](#grounding-and-routing)
* [Fabrication Files](#fabrication-files)

</details>

<details>
<summary><strong><a href="#enclosure-design-and-3d-printing">Enclosure Design and 3D Printing</a></strong></summary>

* [Why Use a Printed Enclosure?](#why-use-a-printed-enclosure)
* [Component-Driven Design](#component-driven-design)
* [Printed Labels and Graphics](#printed-labels-and-graphics)
* [Filament Colors](#filament-colors)
* [Multi-Color Printing](#multi-color-printing)
* [Current Print Status](#current-print-status)

</details>

<details>
<summary><strong><a href="#testing-and-experimental-results">Testing and Experimental Results</a></strong></summary>

* [Breadboard Testing](#breadboard-testing)
* [Frequency-Response Testing](#frequency-response-testing)
* [Clipping Tests](#clipping-tests)
* [Prototype Validation Summary](#prototype-validation-summary)
* [Validation Summary](#validation-summary)

</details>

<p><strong><a href="#planned-additions">Planned Additions</a></strong></p>

<p><strong><a href="README.md">Return to the Main README</a></strong></p>

---

## Design and Prototyping Process

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

This research established a known working baseline and made it possible to evaluate later modifications without losing track of the original circuit behavior.

The part-by-part analysis was also used to identify modern components that could replace less-available original parts while preserving their electrical function.

### 2. Original TS808 Simulation and Breadboard Prototype

The development process began with a publicly available schematic of the original TS808 circuit. That unmodified circuit was first recreated in LTspice and then assembled on a breadboard using the original topology and modern, functionally equivalent components.

Establishing a working unmodified circuit *first* provided a reference against which every later change could be evaluated. Full-size potentiometers, audio jacks, and a Dc barrel jack were integrated into the breadboard during this stage so the circuit could be evaluated as a complete pedal system.

The breadboard stage facilitated the analysis of...

* Basic signal flow
* Input and output buffer operation
* Bias voltages
* Drive-control behavior
* Tone-control behavior
* Level-control behavior
* Symmetric silicon clipping
* Practical operation with a guitar and amplifier

Images were not captured of the original unmodified LTspice circuit or breadboard prototype. However, images shown in the following section display the later circuit after the selected EQ+ modifications had been integrated.

### 3. Frequency-Response and Clipping Experiments

After the original circuit was operating correctly, the breadboard and LTspice models were modified one component and one circuit branch at a time.

The goal was to strike a useful balance between preserving the original TS808 character and adding meaningful tone-shaping options. The modifications were intended to be clearly audible without becoming either extreme or underwhelming.

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

*The circuit shown above is the final LTspice model containing the selected 808 EQ+ modifications, rather than the original unmodified TS808 simulation.*

Much of the Bass Pass Through and Treb Pass Through development involved swapping capacitor and resistor values, adding new components, and testing those components at different points in the signal path.

The Bass Pass Through was designed to let enough low end through to give the guitar a thicker, fuller underbelly without making the distorted low frequencies excessively strong or muddy. The selected configuration lowers the distortion-stage high-pass corner from approximately **720 Hz to 410 Hz**.

The Treb Pass Through was designed to give the pedal a significantly more transparent and open sound without making it excessively harsh or fizzy. The selected configuration raises the tone-stage low-pass corner from approximately **720 Hz to 3.4 kHz**.

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

The purpose of the perfboard stage was to:

* Consolidate the circuit
* Integrate the true bypass foot switch
* Reduce breadboard-related connection problems
* Test the design in a more durable and portable pedal format
* Confirm the final circuit before beginning PCB design

The first enclosure prototype was intentionally faceless and focused primarily on fit and function rather than appearance. It provided a practical way to mount the circuit and controls before committing to the custom PCB and final enclosure design.

The perfboard + test enclosure prototype was used to confirm:

* Basic effect operation
* True bypass functionality
* Drive, Tone, and Level controls
* Bass Pass Through behavior
* Treb Pass Through behavior
* Symmetric silicon clipping
* Asymmetric silicon clipping
* LED clipping
* Switch interaction
* Practical off-board wiring
* Overall sound and usability

This validation established the final circuit configuration transferred to the custom PCB.

The perfboard circuit and faceless enclosure also exposed practical problems that were not as apparent during breadboard testing. These steps were helpful in understanding the intricacies of developing an intuitive, visually appealing, and reliable pedal. They allowed me to refine the physical circuit-assembly process, develop a more compact and easy-to-use enclosure, and configure 3D-printing settings that balanced appearance, dimensional accuracy, and functionality.

*Photos of the perfboard circuit and faceless enclosure prototype will be added here.*

### 5. Component Selection and Price Optimization

Considerable time was spent selecting quality components for the later revisions. This work had to be completed before PCB design because the exact component dimensions, pin spacing, and package styles were required to create or verify footprints and plan the board layout.

Many parts used in the early breadboard and perfboard prototypes came from bulk component variety kits. For the custom PCB revision, the goal was to source only the required parts, reduce unnecessary purchases, improve component consistency, and streamline assembly.

Parts were compared through Octopart and supplier catalogs from DigiKey, LCSC, Tayda Electronics, Mouser, and other vendors. DigiKey was selected as the primary source for on-board electronic components because it offered all the required parts, reputable component quality, reasonable pricing, and the ability to consolidate the order through one supplier.

The available options from these suppliers were less suitable for much of the off-board hardware. Love My Switches was selected for affordable, good-quality potentiometers and mono jacks. The SPDT toggle switches and true-bypass footswitches were purchased through Amazon because they were significantly less expensive and the parts had already proved reliable in the first prototype.

Each supplier was chosen by balancing component cost, quality, availability, and total shipping expense. Enough parts were purchased to build five pedals, which reduced the estimated per-pedal cost through quantity pricing and by spreading shipping costs across multiple builds.

### 6. PCB Design in Altium Designer

The validated circuit was transferred into Altium Designer.

Many schematic symbols and PCB footprints were sourced from DigiKey. These resources were collected, reviewed, corrected where necessary, and assembled into organized project libraries. Custom components were created when a suitable existing symbol or footprint was not available.

Board size and component placement were optimized so the PCB would fit within a compact pedal enclosure. Components belonging to the same functional circuit block were kept near one another, while trace lengths, unnecessary crossings, and layer changes were minimized where practical. Footprint reference designators, value labels, and polarity markings were also aligned and oriented for easy reading during hand assembly and inspection.

The PCB-design process included:

* Collecting and organizing schematic symbols and PCB footprints
* Verifying component pinouts, dimensions, and lead spacing
* Correcting library components where necessary
* Creating custom library components where necessary
* Redrawing the complete schematic
* Assigning components and designators
* Defining the board shape
* Placing through-hole components
* Grouping components by functional circuit block
* Minimizing board area, trace length, and unnecessary trace crossings
* Aligning component labels for efficient assembly and inspection
* Positioning off-board connection pads
* Routing signal and power traces
* Creating top and bottom ground pours
* Running electrical-rule checks
* Running PCB design-rule checks
* Generating fabrication files
* Reviewing the board in 2D and 3D
* Reviewing manufacturer previews

The board uses through-hole components to make hand assembly, inspection, repair, and experimentation more accessible.

Note: Various components can be installed in machine-pin sockets rather than soldered permanently to ease tone experimentation, troubleshooting, and repair. Suggested components include Q1, Q2, U1, C12, C13, and diodes.

### 7. Enclosure Remodeling and Mechanical Integration

The enclosure was remodeled in Fusion after the electronic design and prototype dimensions were better understood.

All enclosure components were modeled specifically for this project. No component models were imported.

The modeled components included:

* Potentiometers
* Toggle switches
* Footswitch
* Input and output jacks
* DC power connector
* PCB
* LED

Nuts, washers, and fasteners were not modeled.

These models made it possible to:

* Optimize component spacing
* Identify mechanical interference
* Plan wire-routing clearance
* Determine opening sizes
* Determine jack and switch depth
* Position the PCB
* Refine the enclosure dimensions
* Improve tool access during assembly

The final enclosure design includes:

* Labels and graphics inlaid flush with the enclosure surface
* Custom printed knobs
* A custom LED holder
* Bottom-cover locating features
* Mounting holes for enclosure-mounted components
* Print-aware wall thicknesses and tolerances
* A small access cutout that makes the bottom plate easier to remove after its screws have been removed

The enclosure does not include an internal PCB mounting or support structure.

### 8. Final Assembly and Testing

The final phase consists of:

* Assembling the manufactured PCB
* Inspecting solder joints
* Verifying power rails and bias voltages
* Testing the PCB outside the enclosure
* Mounting the off-board components
* Completing the off-board wiring
* Performing enclosure fit checks
* Verifying all switch states
* Testing bypass and effect operation
* Evaluating noise, output level, and tone
* Correcting mechanical or electrical issues
* Releasing the final manufacturing and print files

The PCB has been assembled and validated. Final enclosure fit testing and complete pedal validation are still in progress.

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
* Treb Pass Through switching

The Treb Pass Through switch raises the corner frequency of the tone-stage low-pass filter from approximately **720 Hz to 3.4 kHz**.

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

The custom PCB translates the validated prototype into a more durable, reproducible, and serviceable format.

| PCB top                                           | PCB bottom                                              |
| ------------------------------------------------- | ------------------------------------------------------- |
| ![PCB top](Images/Software/Altium_PCB_3D_Top.png) | ![PCB bottom](Images/Software/Altium_PCB_3D_Bottom.png) |

### Design Priorities

The PCB was designed around the following priorities:

* Preserve the validated TS808-style circuit
* Use readily solderable through-hole components
* Keep related circuit stages physically organized
* Provide practical connection points for off-board wiring
* Support component replacement and experimentation
* Fit efficiently within the custom printed enclosure
* Use ground pours to simplify ground distribution
* Provide clear component designators and polarity markings
* Make fabrication possible through common prototype-PCB services

### Library Development

Many schematic symbols and PCB footprints were sourced from DigiKey.

These resources were:

* Collected into project libraries
* Reviewed for dimensional accuracy
* Checked against component datasheets
* Verified for pinout and lead spacing
* Corrected where necessary
* Supplemented with custom components when a suitable model was unavailable

The library work primarily involved assembling, organizing, checking, and adapting available resources rather than creating every component from the beginning.

### Through-Hole Construction

Through-hole components were selected because they are:

* Easier to solder manually
* Easier to inspect visually
* Easier to replace
* Familiar to many hobbyists
* Suitable for machine-pin sockets
* Readily available in small quantities

The larger board area required by through-hole parts was accepted as a worthwhile tradeoff for accessibility and serviceability.

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

### Grounding and Routing

The board uses copper pours on both sides for ground distribution.

Signal traces were routed with attention to:

* Keeping related components close together
* Minimizing unnecessary loop area
* Separating sensitive signal paths from power wiring
* Providing short return paths
* Avoiding interference with through-hole pads
* Maintaining fabrication clearances

Additional detail about the board layout and signal routing will be added after the final revision is fully documented.

### Fabrication Files

The PCB-design process included:

* Redrawing the complete schematic
* Assigning component designators
* Defining the board shape
* Placing through-hole components
* Routing signal and power traces
* Creating top and bottom ground pours
* Positioning off-board connection pads
* Running electrical-rule checks
* Running PCB design-rule checks
* Reviewing the design in 2D and 3D
* Generating fabrication files
* Reviewing manufacturer previews

Physical bare-PCB and assembled-PCB photographs will be added after final documentation is complete.

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
* Longer fabrication time
* Greater dependence on print orientation and tolerances

Common 3D-printing plastics may soften, warp, or deform at temperatures that would not damage a metal enclosure.

### Component-Driven Design

All enclosure-mounted components were modeled specifically for this project, including:

* Potentiometers
* Toggle switches
* Footswitch
* Input and output jacks
* DC power connector
* PCB
* LED

No component models were imported.

The enclosure models did not include nuts, washers, or fasteners.

The modeled components helped determine:

* Hole diameters
* Internal component spacing
* PCB position
* Wire-routing space
* Footswitch clearance
* Jack depth
* Wall thickness
* Bottom-cover geometry
* Tool access during assembly

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

The PCB is not mounted to an internal support structure. Its final position is determined by the connected controls and wiring arrangement.

### Printed Labels and Graphics

The face labels and symbols are integrated into the enclosure model rather than applied afterward.

Contrasting filament is inlaid flush with the enclosure surface. The label geometry is designed to print against the build plate, producing a clean, flat front face without raised or recessed lettering.

A smooth PEI plate was used to improve the finish and readability of the labels.

A textured plate may also work, but it can produce:

* A shinier surface texture
* Less crisp lettering
* More irregular edges
* Blobbier or harder-to-read small text

### Filament Colors

The current design uses:

* **White filament** for most of the enclosure and selected accents on the knobs and LED holder
* **Black filament** for front-face accents and the primary color of the knobs and LED holder

Other colors can be substituted without changing the mechanical design.

### Multi-Color Printing

The enclosure is designed for multi-color printing, but multi-color fabrication is not strictly required.

The Bambu H2S natively supports automatic multi-color printing. However, automated filament changes create purge waste.

Possible alternatives include:

* Printing the enclosure in one color
* Manually changing filament
* Painting the label geometry
* Filling the label geometry after printing
* Printing separate label inserts
* Omitting cosmetic accents

![Sliced enclosure](Images/Software/BambuStudio_Enclosure_Sliced_Iso.png)

### Current Print Status

The most recent enclosure revision has not yet completed final physical validation.

Until testing is complete, the current model should be treated as a design revision rather than a guaranteed final print.

The following files will be added after validation:

* Final Fusion source
* STEP exports
* STL exports
* Dimensional drawings
* Final Bambu Studio project
* Recommended print settings
* Material recommendations
* Assembly notes
* Tolerance and fit notes

---

## Testing and Experimental Results

The circuit was evaluated through simulation, breadboard testing, Analog Discovery 2 measurements, perfboard construction, and practical guitar testing.

This section is intentionally separate from the main README so that detailed graphs and observations can be added without making the project landing page difficult to navigate.

### Breadboard Testing

The original TS808 circuit was first assembled and tested before modifications were introduced.

The breadboard stage was used to:

* Confirm basic circuit operation
* Evaluate modern replacement components
* Compare the physical circuit with LTspice behavior
* Test Drive, Tone, and Level operation
* Experiment with filter values
* Compare diode configurations
* Evaluate switching arrangements
* Test the circuit with a guitar and amplifier

Most of the final potentiometers, jacks, and temporary switching hardware were already used during the breadboard stage.

### Frequency-Response Testing

An Analog Discovery 2 was used to measure the frequency response of the circuit and compare component modifications.

Testing included:

* Original TS808 response
* Bass Pass Through values
* Treb Pass Through values
* Tone-control positions
* Filter corner frequencies
* Gain-stage response
* Tone-stage response

The selected Bass Pass Through configuration shifts the distortion-stage high-pass corner from approximately **720 Hz to 410 Hz**.

The selected Treb Pass Through configuration shifts the tone-stage low-pass corner from approximately **720 Hz to 3.4 kHz**.

Future additions may include:

* Bode plots
* Overlay comparisons
* Test settings
* Component-value tables
* Calculated and measured corner-frequency comparisons

### Clipping Tests

The clipping configurations were evaluated using waveform measurements and practical listening tests.

Testing included:

* Symmetric silicon clipping
* Asymmetric silicon clipping
* Symmetric LED clipping
* Output-amplitude comparisons
* Positive and negative waveform limiting
* Compression and sustain
* Picking dynamics
* Interaction with the Drive control
* Interaction with external boosts and amplifiers

Future additions may include:

* Oscilloscope captures
* Input and output waveform overlays
* Clipping-threshold comparisons
* Harmonic observations
* Level-normalized audio samples

### Prototype Validation Summary

The perfboard prototype was used to confirm:

* Basic effect operation
* Mechanical true bypass
* Drive, Tone, and Level controls
* Bass Pass Through behavior
* Treb Pass Through behavior
* Symmetric silicon clipping
* Asymmetric silicon clipping
* LED clipping
* Switch interaction
* Practical off-board wiring
* Overall sound and usability

The prototype established the circuit configuration transferred to the custom PCB.

### Validation Summary

| Test area                   | Status                   |
| --------------------------- | ------------------------ |
| Original circuit simulation | Complete                 |
| Original breadboard circuit | Complete                 |
| Bass modification           | Prototype verified       |
| Treble modification         | Prototype verified       |
| Symmetric silicon clipping  | Prototype verified       |
| Asymmetric silicon clipping | Prototype verified       |
| LED clipping                | Prototype verified       |
| Perfboard prototype         | Complete                 |
| True-bypass operation       | Prototype verified       |
| Production PCB              | Assembled and validated  |
| Latest enclosure revision   | Final validation pending |
| Complete final pedal        | Final validation pending |

---

## Planned Additions

This document may later include:

* Complete stage-by-stage circuit explanations
* Annotated schematic images
* Filter equations
* Gain calculations
* Bias-voltage measurements
* Analog Discovery 2 Bode plots
* Clipping waveform captures
* LTspice comparisons
* PCB connector assignments
* PCB fabrication notes
* Physical PCB photographs
* Mechanical dimension drawings
* Print orientation diagrams
* Final slicer settings
* Enclosure tolerance notes
* Audio demonstrations
* Final validation results

Return to the [main project README](README.md).
