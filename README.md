# 808 EQ+

A faithful, buildable recreation of the original Tube Screamer 808 circuit with optional bass, treble, and clipping controls.

Most of the 808 EQ+ signal path closely replicates the original TS808 using modern, functionally equivalent components. Its added controls were intentionally designed so they can be switched out of the circuit, allowing the pedal to return to the familiar mid-focused response, symmetric silicon clipping, compression, and sustain associated with a traditional TS808.

When more flexibility is desired, the added switches can extend the pedal’s bass response, open its upper-frequency response, and select between three distinct clipping configurations.

> [!IMPORTANT]
> **Project status:** The circuit and earlier prototypes have been tested. The latest PCB and enclosure revision are currently undergoing final assembly and validation. Final enclosure exports, print files, dimensional drawings, physical build photographs, and complete assembly instructions will be added after testing.

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
* [Repository Contents](#repository-contents)
* [Known Limitations](#known-limitations)
* [Credits and References](#credits-and-references)
* [Disclaimer](#disclaimer)

## Features

* TS808-style signal path using modern, functionally equivalent components
* Ability to return all added tone and clipping controls to a traditional TS808 configuration
* Switchable bass-response extension
* Switchable treble-response extension
* Three selectable diode-clipping configurations
* Original-style Drive, Tone, and Level controls
* Mechanical true-bypass switching
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
* [ ] Latest enclosure revision physically validated
* [ ] Final STEP and STL files released
* [ ] Final Bambu Studio project released
* [ ] Dimensional drawings released
* [ ] Final PCB and pedal photographs added
* [ ] Audio demonstrations added
* [ ] Complete build guide added

---

## What Is the 808 EQ+?

The Tube Screamer is best known for its characteristic mid hump, smooth symmetric clipping, and ability to act as a clean boost that pushes an amplifier while tightening and cleaning up the guitar tone.

The 808 EQ+ preserves that foundation.

Rather than replacing the original TS808 tone, the added controls make it possible to temporarily move beyond it. The bass and treble switches alter specific filter corner frequencies, while the clipping switches change the headroom, compression, volume, and feel of the distortion.

With the added switches returned to their default positions, the pedal can operate much like a traditional TS808.

### Traditional TS808 Character

In its default configuration, the 808 EQ+ provides:

* Reduced bass entering the distortion stage
* Reduced upper treble after the clipping stage
* A pronounced mid-focused response
* Symmetric silicon-diode clipping
* Smooth compression
* Strong sustain
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

This allows the pedal to return to the original bass cut, treble cut, and symmetric silicon clipping that define the traditional Tube Screamer sound.

### Add More Tone-Shaping Flexibility

The original Tube Screamer response is useful because it prevents excessive low frequencies from becoming muddy and limits upper frequencies that might otherwise sound harsh.

However, those same filters can make the pedal feel narrow or overly mid-focused in some rigs.

Several tone-shaping approaches and component values were tested before selecting two modifications:

* A moderate bass extension that adds fullness without allowing the distortion to become excessively muddy
* A substantial treble extension that adds presence, clarity, and sparkle

Both modifications are independently switchable.

### Keep the Project Affordable

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

Detailed documentation for the project’s development process, circuit, PCB, enclosure, printing process, and experimental measurements is maintained separately:

* [Design, Prototyping, and Testing Documentation](DESIGN_AND_TESTING.md)

The separate document includes:

* Complete design and prototyping process
* Signal-path overview
* Circuit-design notes
* PCB construction and routing information
* Socketed and replaceable components
* Enclosure design and mechanical integration
* Multi-color printing considerations
* Testing methodology
* Experimental measurements and validation status

Separating this material keeps the main project page approachable while preserving the engineering detail for readers who want a deeper technical explanation.

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

A complete illustrated build guide will be added after the latest PCB and enclosure revisions complete validation.

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

## Repository Contents

The repository currently uses the following structure:

```text
808_EQ-Plus_Guitar_Pedal/
├── README.md
├── DESIGN_AND_TESTING.md
│
├── Design/
│   ├── 3D_Printing/
│   ├── CAD/
│   ├── LTspice/
│   ├── PCB/
│   ├── 808_EQ-Plus_Single_Pedal_BOM.xlsx
│   └── 808_EQ-Plus_Tools_and_Fabrication_Info.xlsx
│
└── Images/
    └── Software/
        ├── Altium_PCB_3D_Bottom.png
        ├── Altium_PCB_3D_Top.png
        ├── Altium_PCB_Bottom.png
        ├── Altium_PCB_Top.png
        ├── Altium_Schematic.png
        ├── BambuStudio_Enclosure_Sliced_Iso.png
        ├── BambuStudio_Enclosure_Sliced_Topdown.png
        ├── BambuStudio_Enclosure_Sliced_Underside.png
        ├── Fusion_Assembled_Enclosure_Iso.png
        ├── Fusion_Assembled_Enclosure_Top.png
        ├── Fusion_Bare_Enclosure_Inside.png
        ├── Fusion_Bare_Enclosure_Iso.png
        ├── Fusion_Bare_Enclosure_Iso_Exploded.png
        ├── Fusion_Bare_Enclosure_Top.png
        ├── Fusion_Components_Iso.png
        ├── Fusion_Components_Side.png
        ├── Fusion_Components_Top.png
        ├── LTspice_Circuit.png
        └── Perfboard_DIYLayout.png
```

This structure will evolve as final photographs, manufacturing files, drawings, print files, build documentation, and testing results are added.

---

## Known Limitations

* The latest enclosure revision has not yet completed physical fit testing.
* The printed enclosure does not provide the same impact resistance as a cast-metal pedal enclosure.
* Common 3D-printing plastics are generally less resistant to high temperatures than metal enclosures and may soften, warp, or deform if exposed to excessive heat.
* A plastic enclosure does not inherently provide the electromagnetic shielding of a grounded metal enclosure.
* Multi-color printing can produce substantial purge waste.
* The design requires a suitable regulated 9 V center-negative supply.
* The current enclosure does not include a battery compartment.
* Some fabrication and assembly steps require prior soldering, electronics, CAD, or 3D-printing experience.
* Exact sound will vary with the guitar, pickups, amplifier, speakers, signal level, power supply, and playing dynamics.
* Descriptions such as “smooth,” “open,” “gritty,” and “amp-like” are subjective and should not be treated as precise measurements.

---

## Credits and References

The 808 EQ+ is based on the established Tube Screamer 808 circuit topology.

The underlying Tube Screamer circuit was not invented as part of this project. The original contribution of this project is the specific recreation, component selection, switchable modifications, PCB implementation, mechanical design, printed enclosure, documentation, and fabrication workflow.

The project draws on publicly available educational material concerning:

* TS808 circuit analysis
* Op-amp feedback-loop clipping
* Active tone controls
* Transistor buffering
* Analog filter design
* Guitar-pedal bypass wiring
* Through-hole PCB design
* Additive-manufacturing design practices

A detailed reference list and acknowledgments will be added before the final release.

Software and tools used during development include:

* LTspice
* Analog Discovery 2 and WaveForms
* Altium Designer
* Fusion
* Bambu Studio
* Bambu H2S
* General electronic test and soldering equipment

---

## Disclaimer

This project is provided for educational and personal-use purposes.

Build and use it at your own risk. Verify component values, component orientation, diode polarity, transistor pinouts, integrated-circuit orientation, power-supply polarity, operating voltages, and enclosure clearances before connecting the pedal to other equipment.

Disconnect power before modifying the circuit. Avoid making component changes while the pedal is connected to a guitar, amplifier, computer, audio interface, or other valuable equipment.

The design files are still under development and may contain errors or unvalidated revisions.
