# JarvisKeyboard — Lotus58 ZMK Config

Glen Jarvis's personal keymap for the Lotus58 wireless split keyboard.

## Motivation

Switching constantly between Linux and Mac destroyed my muscle memory for copy and paste - I started just right-clicking everything. On top of that, a right AC joint separation meant I had to type one-handed with a mouse in the other hand until I could take off the sling

The Lotus58 solves both problems: mouse movement lives on a keyboard layer, so I never have to reach for a separate mouse. The split design reduces the reach. And, ideally, it will remove the delays of context switching to a mouse.

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
