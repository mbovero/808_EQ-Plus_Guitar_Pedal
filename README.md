# 808 EQ+

A faithful, buildable recreation of the original Tube Screamer 808 circuit with optional bass, treble, and clipping controls.

Most of the 808 EQ+ signal path closely replicates the original TS808 using modern, functionally equivalent components. Its added controls were intentionally designed so they can be switched out of the circuit, allowing the pedal to return to the familiar mid-focused response, symmetric silicon clipping, compression, and sustain associated with a traditional TS808.

When more flexibility is desired, the added switches can extend the pedal’s bass response, open its upper-frequency response, and select between three distinct clipping configurations.

> [!IMPORTANT]
> **Project status:** This project is still in progress. Not all README files are complete, and some sections are still missing information and images. The documentation will continue to be revised and expanded as the remaining prototypes, photographs, demonstrations, and guides are completed.

## Table of Contents

* [Features](#features)
* [Project Status](#project-status)
* [What Is the 808 EQ+?](#what-is-the-808-eq)
* [Why Build Another Tube Screamer?](#why-build-another-tube-screamer)
* [Design Goals](#design-goals)
* [Controls and Operation](#controls-and-operation)

  * [Main Controls](#main-controls)
  * [Tone Switches](#tone-switches)
  * [Clipping Switches and Configurations](#clipping-switches-and-configurations)
  * [Bypass Switching](#bypass-switching)
* [Technical Design and Testing Documentation](#technical-design-and-testing-documentation)
* [Bill of Materials, Tools, and Fabrication Information](#bill-of-materials-tools-and-fabrication-information)
* [Planned Build Process](#planned-build-process)
* [Known Limitations](#known-limitations)
* [Credits and References](#credits-and-references)
* [Disclaimer](#disclaimer)

## Features

* Ability to return all added tone and clipping controls to a traditional TS808 configuration, using modern, functionally equivalent components throughout the circuit
* Independently switchable bass- and treble-response extensions
* Three selectable diode-clipping configurations
* True-bypass switching
* Custom through-hole PCB
* Fully modeled and 3D-printed enclosure
* Custom printed knobs, LED holder, labels, and graphics
* Design files, manufacturing files, and component information for hobbyist construction

## Project Status

* [x] Original TS808 circuit researched and analyzed
* [x] Original circuit simulated
* [x] Original circuit breadboarded
* [x] Tone and clipping modifications evaluated
* [x] Perfboard prototype constructed
* [x] Prototype electrically and audibly validated
* [x] Custom PCB designed
* [x] PCB manufacturing files prepared
* [x] Enclosure modeled
* [x] Latest PCB revision fully assembled and validated
* [x] Latest enclosure revision physically validated
* [x] Final STEP and STL files uploaded
* [x] Final Bambu Studio project uploaded
* [x] Dimensional drawings uploaded
* [ ] Final prototype, PCB, and pedal photographs added
* [ ] Audio demonstrations added
* [ ] Main README, technical documentation, and build guide completed
* [ ] Polished user guide developed

---

## What Is the 808 EQ+?

The Tube Screamer is best known for its characteristic mid hump, smooth symmetric clipping, and ability to act as a clean boost that pushes an amplifier while tightening and cleaning up the guitar tone.

The 808 EQ+ preserves that foundation.

Rather than replacing the original TS808 tone, the added controls make it possible to temporarily move beyond it. The bass and treble switches give the player access to a fuller, clearer sound with more low end and/or upper-frequency detail. The clipping switches change the headroom, compression, volume, and feel of the distortion.

With the added switches returned to their default positions, the pedal can operate like a traditional TS808.

### Traditional TS808 Character

In its default configuration, the 808 EQ+ provides:

* Reduced bass entering the distortion stage
* Reduced upper treble after the tone stage
* A pronounced mid-focused response
* Symmetric silicon-diode clipping
* Moderate compression and sustain
* Familiar Drive, Tone, and Level operation

### Expanded EQ+ Character

The added controls can provide:

* More low-frequency fullness without allowing excessive bass into the distortion stage
* Considerably more treble, presence, and clarity
* Higher-headroom, more dynamic LED clipping
* Asymmetric silicon clipping with slightly greater output and a rougher, more amp-like character

---

## Why Build Another Tube Screamer?

This project began as a way to learn how guitar pedals work internally and to apply the electronics, PCB design, CAD, and manufacturing skills I developed while studying computer engineering in college.

It was also an opportunity to put an existing collection of electronic components, fabrication tools, test equipment, and 3D-printing equipment to practical use.

Commercial guitar pedals can become expensive, especially when experimenting with several variations of a similar circuit. Building the pedal from the component level made it possible to study each circuit stage, experiment with tone-shaping and clipping behavior, and create a pedal tailored to my own preferences.

The idea of creating and sharing a design that could be reproduced, studied, and modified by other hobbyists was also a major motivation for the project.

## Design Goals

### Preserve the Original TS808 Circuit

The original TS808 was chosen as a reliable and well-understood foundation.

The goal was not to loosely imitate its sound or to create an unrelated overdrive with a similar name. The signal path was recreated carefully using modern but functionally equivalent components, and the added modifications were designed so they could be removed from the active signal path through the front-panel switches.

This allows the pedal to return to the original bass cut, treble cut, and symmetric silicon clipping that define the traditional Tube Screamer sound, with familiar Drive, Tone, and Level controls.

### Add More Tone-Shaping Flexibility

The original Tube Screamer response is useful because it prevents excessive low frequencies from becoming muddy and limits upper frequencies that might otherwise sound harsh.

However, those same filters can make the pedal feel narrow or overly mid-focused in some rigs.

Several tone-shaping approaches and component values were tested before selecting two modifications:

* A moderate bass extension that adds fullness without allowing the distortion to become excessively muddy
* A substantial treble extension that adds presence, clarity, and sparkle

Both modifications are independently switchable.

### Keep the Project Affordable and Customizable

A major goal was to reduce the cost of producing a complete pedal.

Traditional die-cast metal pedal enclosures can represent a significant portion of a DIY pedal’s cost. A 3D-printed enclosure reduces that cost while allowing much greater freedom over the enclosure shape, internal structure, labels, colors, mounting features, and overall appearance.

A 3D-printed enclosure can also be customized in ways that would be difficult or expensive with a standard metal box. In principle, the same electronics could be placed in a 3D-printed enclosure shaped like a cloud, mushroom, character, or other custom object.

### Make the Design Educational and Reproducible

The repository is intended for:

* Guitar-pedal enthusiasts with electronics and additive-manufacturing experience
* Electronics hobbyists interested in analog audio circuits
* Guitarists who want to build and modify their own equipment
* Students learning circuit simulation, PCB design, soldering, testing, or CAD
* Curious readers who want to understand how a Tube Screamer works
* Motivated builders who may not yet have enough knowledge to design a pedal independently

This is not intended to be the simplest possible beginner soldering kit. It is a complete engineering project that includes simulation, prototyping, PCB design, off-board wiring, mechanical design, additive manufacturing, and final assembly.

---

## Controls and Operation

### Main Controls

| Control   | Function                                                                                                                                                                                                                                                |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Drive** | Adjusts the gain of the op-amp clipping stage. Higher settings increase signal amplification and drive the clipping diodes harder, producing more distortion and sustain.                                                                               |
| **Tone**  | Controls the balance between the lower-frequency and higher-frequency paths in the TS808 active tone stage. Turning it down emphasizes the filtered, darker signal; turning it up increasingly emphasizes and actively boosts the upper-frequency path. |
| **Level** | Sets the pedal’s final output volume after the clipping and tone stages.                                                                                                                                                                                |

### Tone Switches

| Switch                | Function                                                                                                                                                                                                                                                    |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Bass Pass Through** | Lowers the corner frequency of the high-pass filter in the distortion stage from approximately **720 Hz to 410 Hz**. This allows more bass into the clipped signal, adding fullness and bottom end without completely removing the original bass filtering. |
| **Treb Pass Through** | Raises the corner frequency of the low-pass filter in the tone stage from approximately **720 Hz to 3.4 kHz**. This allows substantially more upper-frequency content through the circuit, increasing clarity, presence, and sparkle.                       |

When both switches are turned off, the original TS808-style bass and treble filtering is restored, producing the familiar Tube Screamer mid hump.

### Clipping Switches and Configurations

The clipping controls use two switches:

| Switch           | Function                                                                                                                                                                               |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Tight / Open** | Selects between silicon-diode clipping and LED clipping. **Tight** engages one of the silicon configurations selected by the Sym/Asym switch. **Open** engages symmetric LED clipping. |
| **Sym / Asym**   | Selects between symmetric and asymmetric silicon clipping while the Tight/Open switch is in the silicon-clipping position.                                                             |

The Sym/Asym switch does not affect the LED configuration.

The clipping diodes are located in the feedback loop of the main op-amp gain stage, as in the original TS808. Each configuration changes the signal level at which clipping begins and the way the positive and negative halves of the waveform are limited.

| Tight/Open | Sym/Asym        | Clipping configuration      | General character                                                                                                                 |
| ---------- | --------------- | --------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Tight**  | **Sym**         | Symmetric silicon clipping  | Traditional TS808-style response. Compressed, smooth, sustained, and relatively even on both halves of the waveform.              |
| **Tight**  | **Asym**        | Asymmetric silicon clipping | Slightly greater output and a less uniform clipping shape. Adds some grit and is often described as feeling more amp-like.        |
| **Open**   | Either position | Symmetric LED clipping      | A much higher clipping threshold provides more headroom, greater output volume, reduced compression, and a more dynamic response. |

### Bypass Switching

The 808 EQ+ uses a mechanical true-bypass footswitch.

When the pedal is bypassed, the guitar signal is mechanically disconnected from the effect circuit and routed directly from the input jack to the output jack. This prevents the pedal’s active input and output buffers from affecting the bypassed guitar signal.

---

## Technical Design and Testing Documentation

Detailed documentation for the project’s development process and major design stages is maintained separately:

* [Design, Prototyping, and Testing Documentation](DESIGN_AND_TESTING.md)

The separate document includes:

* Complete design and prototyping process
* In-depth circuit design
* PCB construction
* Enclosure design and mechanical integration
* 3D Printing considerations
* And plenty of information for curious minds

This material is separated to keep the main project page more approachable while preserving a deeper technical explanation for interested readers.

---

## Bill of Materials, Tools, and Fabrication Information

Detailed component quantities, part numbers, vendor links, estimated prices, and fabrication information are provided in:

* [`808_EQ-Plus_Single_Pedal_BOM.xlsx`](Design/808_EQ-Plus_Single_Pedal_BOM.xlsx)
* [`808_EQ-Plus_Tools_and_Fabrication_Info.xlsx`](Design/808_EQ-Plus_Tools_and_Fabrication_Info.xlsx)

### Bill of Materials

The single-pedal BOM is intended to identify the components required to produce one complete pedal.

Depending on availability, many parts can be replaced with electrically and mechanically compatible alternatives.

Substitutions should account for:

* Electrical value
* Voltage and power rating
* Pinout
* Package dimensions
* Lead spacing
* Polarity
* Tolerance
* Mechanical fit
* Expected effect on the audio circuit

### Tools and Equipment

Not every item listed in the tools and fabrication spreadsheet is required.

Some tools are optional conveniences, some can be replaced with equivalent products, and others are only necessary when modifying or troubleshooting the design.

Examples of potentially optional items include:

* Tweezers
* Solid-core hookup wire
* Solder sucker
* Multiple filament colors
* Smooth build plate
* Dedicated bench power supply
* Advanced measurement equipment

A basic build requires suitable soldering equipment, common hand tools, a way to produce the PCB and enclosure, and a safe method of testing the completed circuit.

---

## Planned Build Process

A complete illustrated build guide will be added as the remaining project documentation is completed.

The planned process is:

1. Review the schematic, BOM, and build documentation.
2. Order or fabricate the PCB.
3. Obtain and inspect all electronic components.
4. Print the enclosure, bottom cover, knobs, and LED holder.
5. Confirm that printed parts and enclosure-mounted components fit correctly.
6. Populate the lowest-profile PCB components.
7. Install sockets for selected experimental components.
8. Populate the remaining through-hole components.
9. Inspect component orientation and solder joints.
10. Test the power input and bias network.
11. Verify important DC operating points.
12. Test the populated PCB outside the enclosure.
13. Mount the potentiometers, switches, jacks, LED, and footswitch.
14. Complete the off-board wiring.
15. Re-test the circuit before mounting the PCB.
16. Mount and secure the PCB.
17. Close the enclosure and inspect for mechanical interference.
18. Verify bypass operation.
19. Test every control and switch combination.
20. Perform final guitar and amplifier testing.

---

## Known Limitations

### Hobbyist 3D-Printed Enclosure Considerations

* The printed enclosure does not provide the same impact resistance as a cast-metal pedal enclosure.
* Common 3D-printing plastics are generally less resistant to high temperatures than metal enclosures and may soften, warp, or deform if exposed to excessive heat.
* A plastic enclosure does not inherently provide the electromagnetic shielding of a grounded metal enclosure.
* Print quality and dimensional accuracy will vary depending on the 3D printer, material, calibration, and print settings used. I cannot guarantee that every print will be suitable for mounting components or that all printed text will be legible.
* The current enclosure does not include a battery compartment.

### Electronics and Assembly Considerations

* The design requires a suitable regulated 9 V center-negative supply.
* Some fabrication and assembly steps require prior soldering, electronics, CAD, or 3D-printing experience.

### Variations in Sound and Interpretation

* Exact sound will vary with the guitar, pickups, amplifier, speakers, signal level, power supply, and playing dynamics.
* Descriptions such as “smooth,” “open,” “gritty,” and “amp-like” are subjective and should not be treated as precise measurements.

---

## Credits and References

### Project Basis and Attribution

The 808 EQ+ is based on the established Tube Screamer 808 circuit topology. The underlying Tube Screamer circuit was not invented as part of this project.

The original contributions of this project include the specific circuit recreation, modern component selection, switchable tone and clipping modifications, PCB implementation, mechanical design, printed enclosure, documentation, and fabrication workflow.

Development drew on educational material covering TS808 circuit analysis, op-amp feedback-loop clipping, active tone controls, transistor buffering, analog filter design, guitar-pedal bypass wiring, through-hole PCB design, and additive-manufacturing practices.

### Primary References

Two resources were particularly helpful during the early research and circuit-analysis stages:

* [**ElectroSmash**](https://electrosmash.mas-effects.com/) — The ElectroSmash Tube Screamer analysis provided a detailed stage-by-stage explanation of the original circuit, including its operating theory, filter behavior, gain calculations, clipping, buffering, and tone control.
* [***Tracking Down Your Dream Tone — Build Your Own Guitar Effects Pedals: A Beginner’s Guide***](https://www.amazon.com/dp/B09ZCJLB9J) by Sascha Suhr — This book provided an accessible introduction to guitar-pedal electronics, circuit simulation, breadboard experimentation, component selection, practical construction, and troubleshooting.

### Additional Online Resources

The following websites, channels, and community forums were also consulted for circuit references, practical building information, equipment demonstrations, troubleshooting discussions, and perspectives from other pedal builders and guitarists:

* [Beavis Audio Research](https://beavisaudio.com/)
* [Analog Man](https://www.analogman.com/)
* [That Pedal Show](https://www.youtube.com/thatpedalshow)
* [GEO’s Effects](http://www.geofex.com/)
* [Free Stompboxes](https://www.freestompboxes.org/)
* [DIY Stompboxes](https://diystompboxes.com/wpress/)
* [PedalPCB Community Forum](https://forum.pedalpcb.com/)
* [The Gear Page](https://www.thegearpage.net/)

Community discussions and subjective descriptions were used as practical references rather than definitive technical sources. Circuit behavior and design decisions were evaluated through component datasheets, circuit analysis, simulation, electrical measurements, and hands-on listening tests.

### Software and Development Tools

Software and equipment used during development included:

* LTspice
* Analog Discovery 2 and WaveForms
* Altium Designer
* Autodesk Fusion
* Bambu Studio
* Bambu H2S
* General electronic test, soldering, and assembly equipment

---

## Disclaimer

This project is provided for educational and personal-use purposes.

Build and use it at your own risk. Verify component values, component orientation, diode polarity, transistor pinouts, integrated-circuit orientation, power-supply polarity, operating voltages, and enclosure clearances before connecting the pedal to other equipment.

Disconnect power before modifying the circuit. Avoid making component changes while the pedal is connected to a guitar, amplifier, computer, audio interface, or other valuable equipment.

The repository may contain mistakes, and reports of any inconsistencies or errors would be greatly appreciated.
