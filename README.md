# BassStudio

**BassStudio** is a Windows desktop application for bassing music, previewing changes, and editing specific sections of a track without having to reprocess the entire song.

The program is being developed in **C# with Visual Studio** and is intended to provide a simple graphical workflow for bass enhancement, frequency replacement, waveform-based editing, and final audio export.

> **Project status:** Active development

---

## Features

- Load audio tracks into a Windows desktop interface
- Display the track as an interactive waveform
- Re-bass an entire song
- Select a specific section of the waveform for editing
- Apply different bass settings to selected sections
- Replace or modify bass only where needed
- Stitch the edited section back into the processed song
- Preview audio before exporting
- Adjustable bass parameters
- Resizable interface panels / tiles
- Windows-native desktop application
- Visual Studio project structure

---

## Waveform Section Editing

One of the main goals of BassStudio is to make it easy to correct sections of a song where a single bass configuration does not sound right.

Instead of processing the entire track again, the workflow is designed around selecting part of the waveform:

1. Load a song.
2. Apply the main bass settings.
3. Highlight a section of the waveform.
4. Adjust the bass settings for only that section.
5. Preview the selected section.
6. Apply the edit.
7. BassStudio stitches the modified section back into the rest of the processed song.
8. Export the completed track as one continuous audio file.

This makes it possible to use different bass frequencies or processing strengths throughout the same song.

---

## Typical Use Cases

BassStudio can be useful when:

- One part of a song needs deeper bass than another
- A bass note does not reproduce well on a particular subwoofer system
- Different sections need different replacement frequencies
- A bassed track has a section that clips or becomes distorted
- You want to experiment with bass frequencies without modifying the entire song
- You want to create a customized version of a track for a specific audio system

---

## Requirements

### Development

- Windows 10 or Windows 11
- Visual Studio
- .NET / C#
- Windows desktop development workload

The exact .NET version and third-party dependencies may change while the project is under active development.

### Runtime

A normal Windows PC capable of decoding and processing the selected audio format.

---

## Building From Source

1. Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/BassStudio.git
```

2. Open the solution in Visual Studio.

```text
BassStudio.sln
```

3. Restore any required NuGet packages.

4. Select:

```text
Release | Any CPU
```

or the appropriate target architecture.

5. Build the solution.

6. Run `BassStudio.exe` from the build output directory.

---

## Project Structure

A typical project layout is:

```text
BassStudio/
├── src/
│   └── BassStudio/
│       ├── MainForm.cs
│       ├── MainForm.Designer.cs
│       ├── Program.cs
│       └── ...
├── README.md
└── BassStudio.sln
```

The structure may change as the audio-processing engine and waveform editor continue to be developed.

---

## Audio Processing Workflow

The basic processing pipeline is:

```text
Original Audio
      │
      ▼
Audio Decode
      │
      ▼
Waveform Display
      │
      ├──────────────► Full Track Processing
      │
      └──────────────► Selected Region Processing
                              │
                              ▼
                       Bass Modification
                              │
                              ▼
                        Region Replacement
                              │
                              ▼
                         Final Audio Mix
                              │
                              ▼
                            Export
```

---

## Region-Based Processing

Internally, section editing can be thought of as three pieces:

```text
[ Before Selection ] [ Selected Region ] [ After Selection ]
```

Only the selected region needs to be reprocessed.

After processing:

```text
[ Original/ed Audio ]
          +
[ Modified Selected Region ]
          =
[ Final Continuous Track ]
```

Crossfading or boundary smoothing can be used at the beginning and end of a modified region to prevent clicks or abrupt changes.

---

## Planned Features

Features being considered or developed include:

- Multiple editable waveform regions
- Per-region bass frequency settings
- Per-region gain controls
- Undo / redo
- Zoomable waveform
- Drag-to-select waveform regions
- Selection start/end time display
- Loop selected section during preview
- Copy settings between regions
- Preset system
- Save and reopen projects
- Non-destructive editing
- Automatic crossfades between modified regions
- Clipping detection
- Peak normalization
- Output limiter
- Batch processing
- Additional audio format support
- Improved waveform rendering
- Processing progress display
- Before/after A/B preview

---

## Audio Preview

BassStudio uses Windows audio playback for preview functionality.

Some Windows playback APIs only accept uncompressed PCM WAV data. Audio formats such as MP3, AAC, FLAC, or compressed WAV formats may therefore need to be decoded to PCM before being sent to the preview engine.

The long-term goal is for preview playback to transparently handle the supported source formats.

---

## Non-Destructive Editing

The preferred editing model is non-destructive.

The original audio should remain unchanged while BassStudio keeps track of:

- Selection position
- Selection length
- Bass frequency
- Gain
- Processing parameters
- Replacement settings

The final file is rendered only when the user exports the track.

This makes it possible to continue adjusting individual sections without permanently changing the source file.

---

## Example Editing Session

```text
00:00 ─────────────────────────────────────────────── 04:12

       Main bass settings applied to entire track

01:14 ─────── 01:27
       Selected region
       Bass frequency changed

02:03 ───────────── 02:22
       Selected region
       Gain reduced

03:41 ───── 03:49
       Selected region
       Different bass replacement applied

Final Export:
All processed regions are rendered into one continuous song.
```

---

## Development Goals

The goal of BassStudio is to provide a workflow that is easier to use than manually cutting audio into multiple files, processing each piece separately, and joining them back together.

The program should eventually allow a user to perform the entire workflow visually:

```text
Load → Bass → Highlight → Adjust → Preview → Apply → Export
```

---

## Known Development Areas

Because BassStudio is still under development, some parts of the application may change significantly.

Current development areas include:

- Audio preview compatibility
- Waveform selection behavior
- Section replacement and stitching
- UI resizing
- Processing performance
- Audio format compatibility
- Export quality
- Seamless transitions between differently processed sections

---

## Contributing

Contributions, testing, bug reports, and feature suggestions are welcome.

When submitting an issue, include:

- Windows version
- BassStudio version or commit
- Audio file format
- Sample rate / bit depth if known
- Steps to reproduce the problem
- Error message or stack trace
- Screenshots when useful

For audio-processing bugs, a short description of the expected and actual result is especially helpful.

---

## Bug Reports

Please use the GitHub **Issues** section for bugs.

A useful bug report looks like:

```text
Version:
Windows Version:
Audio Format:
Sample Rate:
Bit Depth:

Steps:
1.
2.
3.

Expected Result:

Actual Result:

Error / Stack Trace:
```

---

## Disclaimer

BassStudio is an experimental audio-processing project.

Always keep a copy of the original audio file. Processing parameters that add substantial low-frequency energy can cause clipping or place additional stress on amplifiers, speakers, and subwoofers.

Use appropriate gain structure and audio-system protection.

---

## License

- GPLv3

---

## Author

BassStudio is an independent Windows audio-processing project.

---

## Screenshots


![bassstudio main](https://github.com/brianbri6/bassstudio/blob/main/bassstudio.jpg)
```

---

## Roadmap

The main development direction is:

** an entire track, visually select any problem area, apply custom settings only to that area, and seamlessly integrate the edited section back into the finished song.**
