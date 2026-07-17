# 808 EQ+

A faithful, buildable recreation of the original Tube Screamer 808 circuit with optional bass, treble, and clipping controls.

Most of the 808 EQ+ signal path closely replicates the original TS808 using modern, functionally equivalent components. Its added controls were intentionally designed so they can be switched out of the circuit, allowing the pedal to return to the familiar mid-focused response, symmetric silicon clipping, compression, and sustain associated with a traditional TS808.

When more flexibility is desired, the added switches can extend the pedal’s bass response, open its upper-frequency response, and select between three distinct clipping configurations.

> [!IMPORTANT]
> **Project status:** This project is still in progress. Not all README files are complete, and some sections are still missing information and images. The documentation will continue to be revised and expanded as the remaining prototypes, photographs, demonstrations, and guides are completed.

## Table of Contents

* [Project Status](#project-status)
* [What Is the 808 EQ+?](#what-is-the-808-eq)
* [Why Build Another Tube Screamer?](#why-build-another-tube-screamer)
* [Design Goals](#design-goals)
* [Feature List](#feature-list)
* [Controls and Operation](#controls-and-operation)
* [Technical Documentation](#technical-documentation)
* [Build Your Own 808 EQ+](#build-your-own-808-eq)
* [Warnings and Limitations](#warnings-and-limitations)
* [Credits and References](#credits-and-references)
* [Disclaimer](#disclaimer)

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
* LED clipping with more headroom for dynamic distortion
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

## Feature List

The 808 EQ+ pedal's primary features include:

* Traditional TS808-style operation when the added tone and clipping controls are returned to their default positions
* Modern, functionally equivalent components throughout the circuit
* Independently switchable bass- and treble-response extensions
* Three selectable diode-clipping configurations
* Mechanical true-bypass switching
* Custom through-hole PCB
* Fully modeled and 3D-printed enclosure
* Custom-printed knobs, LED holder, labels, and graphics
* Design files, manufacturing files, and component information for hobbyist construction


---

## Controls and Operation

The 808 EQ+ uses three knobs, four toggle switches, and a true-bypass footswitch.

| Control | What it does |
| --- | --- |
| **Drive** | Sets the amount of distortion. Turn it up for more grit, compression, and sustain. |
| **Tone** | Adjusts the pedal from darker and smoother to brighter and more present. |
| **Level** | Sets the final output volume. Start low and adjust it to match or boost the volume with the effect engaged. |
| **Tight / Open** | Selects a focused, more compressed sound or a louder, more dynamic sound. |
| **Sym / Asym** | Changes the texture of Tight-mode distortion from smoother and more even to thicker and grittier. This switch has no effect in Open mode. |
| **Cut / Treb** | Selects the traditional smoother treble response or adds clarity, presence, and sparkle. |
| **Cut / Bass** | Selects the traditional tighter low end or adds fullness and weight. |
| **Footswitch** | Turns the effect on or off. The LED lights while the effect is active; when it is off, the pedal uses true bypass. |

For the familiar TS808-style sound, flip all four toggle switches upward to select **Tight**, **Sym**, and both **Cut** settings. Lower the Level control before switching to Open mode because it can produce substantially more output.

For connection diagrams, detailed mode descriptions, recommended starting settings, power information, and troubleshooting help, see the [808 EQ+ User Manual](808_EQ-Plus_User_Manual.pdf).

---

## Technical Documentation

Detailed documentation for the project’s development process and major design stages is maintained separately:

* [Design, Prototyping, and Testing Documentation](TECHNICAL_DOCUMENTATION.md)

The separate document includes:

* Complete design and prototyping process
* In-depth circuit design
* PCB construction
* Enclosure design and mechanical integration
* 3D Printing considerations
* And plenty of information for curious minds

This material is separated to keep the main project page more approachable while preserving a deeper technical explanation for interested readers.

---

## Build Your Own 808 EQ+

If this project has made you curious about building an 808 EQ+ of your own, you are welcome to use the repository as a DIY construction resource. The project is intended for hobbyists who want to assemble the documented design, learn from it, or adapt it to suit their own ideas.

At a high level, the process involves reviewing the schematic and bill of materials, choosing between the provided PCB and a perfboard build, obtaining the components, printing and checking the enclosure parts, assembling and testing the electronics, installing the off-board controls and connections, and completing final mechanical and functional checks with a guitar and amplifier.

The complete [808 EQ+ DIY Build Guide](BUILD_GUIDE.md) brings together the component and tool lists, fabrication resources, PCB and perfboard options, recommended print settings, assembly guidance, staged testing, and troubleshooting information. Read through the guide before ordering parts or beginning construction.

---

## Warnings and Limitations

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
