# MidiConvert

## Description

Extended version of conner_bw's original midi convert tool, including danoise's additions from 2017. It extends the export of the tool, including pitchbend, aftertouch, vsti parameter and midi cc automation, which makes it very handy to convert your song to common pianoroller daws.

Original tool: https://www.renoise.com/tools/midi-convert
Danoise changes: https://github.com/renoise/xrnx/commits/master/Tools/com.renoise.MidiCon...

Includes the following additions to the export of the tool:

- midi control device automation support -> MIDI CC 21 - 31 (max. 10 parameters per instrument)
- instr. automation device support -> MIDI CC 103 - 113 (max. 10 parameters per instrument)
- pattern midi pitchbend
- pattern midi pitchbend -> MIDI CC 20 (for DAWs not supporting pitchbend import…)
- pattern channel aftertouch
- pattern channel aftertouch -> MIDI CC 102 (for DAWs not supporting pressure import…)
- sequence slot mute support
- sequence slot mute -> note off support
- corrected LPB
- Track names also contain Renoise track names
- Numbering is now in Hex
- Sequence comments -> marker support (buggy, actually didn’t find a DAW supporting it at import)
- Actual midi channel used now
- Instr.-/midi-/plugin-transpose support

You can then copy the automation from the imported MIDI CC lane to the correct VSTi’s automation lane.

Keep in mind the following limitations/requirements before exporting a song:

- Only use one instrument per track
- Always use only one midi control device and one instr. automation device per instrument
- Put the devices always onto the track where the instrument plays
- Max. 10 automated parameters in automation devices, position doesn’t matter
- Always start with the first instrument at position 00, don’t leave an instrument slot empty
- Try to end all notes with note-off somewhere at least. You also can use a following muted slot.

Still alpha. Please deactivate the original com.renoise.midiconvert tool, before using this one. For bug reports, send me a message @ffx in the forum.


## Original Description

Converts a Renoise song into a MIDI file. Notes are grouped by instrument and exported per track.

The tool creates a menu entry called "Export Song to MIDI..." in the File menu, "Selection:Export to MIDI..." in the Pattern Editor menu, and an "Export Selection to MIDI" keybinding.

## Contributing

The code is decently commented, includes a generic Midi.lua class that can be reused for other tasks. Patches are welcome.

## Links

**Tool page (download)**: https://www.renoise.com/tools/midi-convert-w-extended-export
**Renoise Forum (discussion)**: http://forum.renoise.com/index.php/topic/28569-new-tool-30-midi-convert/

## Implemented Effect Commands:

### Pattern Commands
* ZTxx: Set BPM
* ZLxx: Set LPB
* ZKxx: Set TPL
* 0Qxx: Delay all notes by xx ticks

### MIDI Commands
* M0 xxyy: Set CC Number/Value

### Volume Column
* 00-80: Set volume of note
* Qx: Delay note for x ticks
* Cx: Cut note after x ticks

### Panning Column
* Qx: Delay note for x ticks
* Cx: Cut note after x ticks

### Delay Column
* 0-FF: Delay note


## Changelog

0.96
- Proper support for Renoise LPB commands
- Allow MIDI-CC Commands without accompanying note
- Allow notes spanning multiple patterns

0.95
- Adds support for MIDI-CC Commands

0.94
- Updated manifest.xml for compatibility with Renoise 3.1

0.92+0.93
- Fix where multiple consecutive notes could appear with zero length

0.91
- Updated manifest.xml for compatibility with Renoise 3.0