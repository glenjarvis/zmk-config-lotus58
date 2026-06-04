# JarvisKeyboard — Lotus58 ZMK Config

Glen Jarvis's personal keymap for the Lotus58 wireless split keyboard.

## Display

The display has these components, from top to bottom:

- **Battery indicator** (upper left)
- **Communication method icon** — a single icon showing how the keyboard is
  currently talking to the host. Only one of these appears at a time:
  - **Wi-Fi symbol:** Connected over Bluetooth (Low Energy). Despite the icon,
    this is *not* real Wi-Fi — it's the standard ZMK way of showing a BLE
    connection.
  - **USB symbol:** Connected over a wired USB-C connection.
  - **Gear symbol:** The selected Bluetooth profile is in pairing mode —
    advertising and awaiting a connection from a host.
  - **X symbol:** Not connected. This covers a profile that's paired but
    currently disconnected, as well as the case where no output is selected at
    all.
- **Five profile indicators** — one per ZMK Bluetooth profile, laid out as:
```
   1   2
     3
   4   5
```
- **Layer title** — the name of the active layer, shown at the bottom of the
  display below everything else.

### Profile indicators

The five numbers map directly to the five ZMK Bluetooth profiles that the
keyboard supports (e.g., Computer #1 is paired to profile 1, Computer #2 to
profile 2, etc.). The keyboard can only have one active output at a time, so
only one profile is ever selected.

Each indicator combines two independent visual elements:

- **The number's background (active profile):** By default a number sits on a
  black background. The currently selected profile is drawn as a black number on
  a solid white circle.
- **The ring (pairing and connection state):** Around the circle is a ring that
  shows the state of the external device for that profile. These rings are
  always visible, even for profiles that aren't currently selected:
  - **No ring:** Nothing is paired to that profile.
  - **Solid ring:** The device is paired and actively connected.
  - **Dashed ring:** The device is still paired, but not currently connected.

These two elements are independent: a profile can be the active one (white
circle) while still showing a dashed ring, meaning it's selected as the output
but the device isn't currently connected.


## Motivation

Switching constantly between Linux and Mac destroyed my muscle memory for copy
and paste - I started just right-clicking everything. On top of that, a right
AC joint separation meant I had to type one-handed with a mouse in the other
hand until I could take off the sling

The Lotus58 solves both problems: mouse movement lives on a keyboard layer, so
I never have to reach for a separate mouse. The split design reduces the reach.
And, ideally, it will remove the delays of context switching to a mouse.

I got mine from Jake on Etsy - great keyboard and incredible customer service:
[Lotus58 Split Wireless Keyboard](https://www.etsy.com/listing/4393228481/lotus58-split-wireless-keyboard)

## Flashing (macOS)

Files downloaded from GitHub have macOS extended attributes. Standard `cp` tries to copy them, the UF2 bootloader rejects them, and the flash fails silently. Always use `cp -X`:

```bash
# Flash right half first
cp -X firmware_right.uf2 /Volumes/NICENANO/

# Then flash left half
cp -X firmware_left.uf2 /Volumes/NICENANO/
```

After a settings reset (clears Bluetooth pairing and ZMK Studio overrides):

```bash
cp -X settings_reset-nice_nano_v2.uf2 /Volumes/NICENANO/
# wait for reboot, then re-flash firmware
```
