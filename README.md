# UMP-Monitor

A modern, cross-platform MIDI monitor built around **MIDI 2.0 / Universal MIDI Packet (UMP)**: a MIDI-OX for the MIDI 2.0 era.

Every message, whether it comes from a MIDI 1.0 port or a native UMP endpoint, is normalised to UMP and decoded:
MIDI 1.0 and MIDI 2.0 Channel Voice, System, SysEx7/SysEx8 (with MIDI-CI recognition), Mixed Data Sets,
Flex Data (tempo, time/key signature, metadata and lyrics) and UMP Stream (endpoint and function block discovery).

## Run it

Requires the .NET 10 SDK.

```sh
dotnet run --project src/UmpMonitor.App            # normal start
dotnet run --project src/UmpMonitor.App -- --demo  # opens the built-in demo sources right away
dotnet test                                        # decoder/converter tests
```

## Features

- Live list with timestamp, source, group, channel, type, message, decoded details and raw UMP words
- RAW view: each packet as hex with every spec field highlighted by role (type, group, status, channel, note/index, value, flags, data, reserved). Hovering a field shows its spec name, what it does, its bit position and its decoded value. Reserved bits that aren't zero are flagged in red
- Field-by-field breakdown of the selected packet (16/32-bit values, Pitch 7.9 attributes, RPN names, FB info, …)
- Filters by message family, channel and free text; optional hiding of Timing Clock / Active Sensing
- Group × channel activity matrix
- CSV export of the visible messages
- Demo sources (MIDI 2.0 synth and MIDI 1.0 keyboard) to explore without hardware

## License

MIT, see [LICENSE](LICENSE).

## Roadmap

- Native UMP on macOS via `MIDIInputPortCreateWithProtocol`
- Hot-plug via `MidiEndpointDeviceWatcher` instead of the Refresh button; device timestamps instead of arrival time
- Outputs: send messages, MIDI-OX-style routing/thru between ports
- SysEx reassembly view and a MIDI-CI inspector (Discovery, Profiles, Property Exchange JSON)
- Session logging to file, saved filter presets, configurable C3/C4 octave naming
