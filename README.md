# FF_AV_mod for Nintendo Famicom

A modification board for the original Nintendo Famicom that combines an improved video output, audio processing with pseudo-stereo, and a separate regulated power supply.
The board is designed to replace the RF modulator inside the original Famicom and connects directly to the PPU, the CPU audio outputs, the cartridge connector, and the stock power button. It can also be used to modify Famicom clones that use the large-package CPU and PPU chips.

![Mod board](https://github.com/Viva76/FF_AV_mod/blob/main/Images/FF_AV_mod.jpg)

> **Important:** before installing, make sure the console is fully functional and in good working order.

## Features

- Composite video signal generated from the PPU via the **BA7622F**.
- AV output via a **Mini-DIN-4** connector.
- Audio processing based on a dual **4558** operational amplifier.
- Separate left and right audio channels for pseudo-stereo.
- Input diode bridge for reverse-polarity protection.
- Separate **LM2596**-based power regulator, in two variants:
  - adjustable **LM2596-ADJ**;
  - fixed **LM2596-5.0**.
- Additional filtering of the +5 V rail and a separate filtered `+5VA_1` supply for the analog section.
- Diagnostic connection for checking the stock video output before final assembly.
- The power, video, and audio connectors are designed so that the console case does not need to be modified.


### 1. Power Supply

The board has a separate **LM2596**-based power converter and an input diode bridge. The input supply voltage can be of either polarity, in the range of 9 to 12 V.

Two configurations are provided, depending on the LM2596 version used.

#### LM2596-ADJ

Install:

- `R9`;
- `R10`;
- `C6`;

as shown in the schematic.

#### LM2596-5.0

For the fixed 5 V regulator:

- do not install `R10`;
- do not install `C6`;
- install a **0 Ω** jumper in place of `R9`.

Additional power filtering follows the regulator, along with a separate filtered analog rail, `+5VA_1`.

> **Warning:** before connecting the console electronics, always check the regulator's output voltage with a multimeter.

---

## 2. Connecting Power and the Power Button

Connect the Famicom mainboard to the mod board via `J4` or `J5`, following the markings on the PCB.

The wires from the stock power button must be extended and connected to:

```text
J2 — PWR_sw
```

Before connecting the console electronics, be sure to measure the regulator's output voltage with a multimeter.

---

## 3. Diagnostic Video Connection

`JP3` and `C5` form a diagnostic section that allows you to check the console's stock video output after power is connected and the VA signals are connected to `JP4` or `JP5`.

This section is **not required for normal operation of the mod**.

Recommended procedure:

1. If the console is known to be working, leave `C5` uninstalled and `JP3` open.
2. If diagnostics are needed, install `C5` and close `JP3`.
3. Check the operation of the stock video output.
4. After the check, be sure to remove `C5` and open `JP3` before final assembly.

---

## 4. Composite Video

The video signal is taken directly from **PPU pin 21** and fed to `J7` (`Video_21_in`).

The signal then passes through the video path built around the **BA7622F**. The board lets you select which input of the chip is used.

### Connecting the PPU Video Signal to the Mod Board

Locate **PPU pin 21**.

Connect:

```text
PPU pin 21
    │
    └──── shielded wire ────> J7 / Video_21_in
```

The wire should be as short as possible and routed so as to minimize interference. A **shielded wire** is recommended. To reduce vertical stripes, it is also recommended to lift PPU pin 21 off the board.


### Connecting the Video Output

Select **IN1** or **IN2** using the corresponding configuration of jumpers and capacitors.

For IN1:

```text
JP1 = CLOSED
C3  = INSTALLED
JP2 = OPEN
C4  = NOT INSTALLED
```

For IN2:

```text
JP1 = OPEN
C3  = NOT INSTALLED
JP2 = CLOSED
C4  = INSTALLED
```
The **BA7622F** video buffer channels **IN1** and **IN2** have identical characteristics; the redundancy is provided in case one channel of the chip turns out to be faulty.

---

## 5. Audio / Pseudo-Stereo

The audio path is built around the **4558** dual operational amplifier.

The board receives the following audio signals:

- `SND_1` — the first CPU audio output;
- `SND_2` — the second CPU audio output;
- `SND_46` — the audio signal from the cartridge connector.

After processing, two separate channels are produced:

- `AudioL` — left channel;
- `AudioR` — right channel.

To connect, you need to:

1. On the cartridge connector, carefully **cut the trace leading to pin 45**.
2. Remove the resistor dividers on CPU audio outputs **1 and 2**.
3. Connect CPU pins 1 and 2 to the corresponding inputs of the board's audio path:
	```text
	CPU audio output 1 ───> SND_1
	CPU audio output 2 ───> SND_2
	```

For the audio connections, shielded wire is also recommended to reduce interference.

> The exact component locations must be verified against the schematic for your specific Famicom revision.

---

## 6. AV Cable

A **Mini-DIN-4** connector is used for connection.

A ready-made Mini-DIN → RCA adapter can be used. For a snug fit, some ready-made adapters may require trimming the plastic housing by approximately **2 mm**.

---

## 7. Connectors

| Connector | Purpose |
|---|---|
| `J1` | Power input |
| `J2` | `PWR_sw` — connection for the stock power button |
| `J3` | Mini-DIN-4 AV output |
| `J4` | Power/signal connection for console revision HVC-CPU-GPM-02 |
| `J5` | Power/signal connection for console revision HVC-CPU-07 |
| `J6` | Audio signal inputs |
| `J7` | PPU video signal input, pin 21 |

`J4` and `J5` are alternative connection points to the console mainboard. Use whichever is more convenient for routing the wires inside the case.

---

## Project Files and Documentation

* 📄 **[Device schematic (PDF)](https://github.com/Viva76/FF_AV_mod/blob/main/docs/schematic.pdf)**
* 📋 **[Bill of materials (BOM)](https://Viva76.github.io/FF_AV_mod/ibom.html)**
* 📦 **[Gerber files for ordering the PCB](https://github.com/Viva76/FF_AV_mod/blob/main/Gerber/FF_AV_mod_Gerbers.rar)**

---

## Gallery and Installation Examples

[Gallery with examples](https://github.com/Viva76/FF_AV_mod/tree/main/Images/)

---

## Disclaimer

This project is intended for hardware modification of the original Nintendo Famicom. Installation requires soldering, connecting to the console's original mainboard, and altering the cartridge connector circuit.

Incorrect installation may damage the console, the mod board, or connected equipment.

Before starting work, make sure you understand the possible risks and know how to check electrical connections and voltages with a multimeter.
