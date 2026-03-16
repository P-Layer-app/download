# P-Layer

P-Layer is a professional broadcast automation application designed for radio stations, community radio, and streamers. It provides precise playlist control, audio processing, scheduling, streaming (Icecast/Shoutcast), and integrated Voice Tracking.

![P-Layer Screenshot](screen1.png)

![P-Layer Screenshot](screen2.png)

![P-Layer Screenshot](screen3.png)
---

## Key Features

- Broadcast automation and playlist control
- **Rotator** music scheduling system
- Automatic daily playlist generation (.m3u) from hourly clocks
- Visual hour editor (**Clock Wheel**)
- Artist / Track separation rules for music rotation
- Integrated **Voice Tracking**
- Audio processing and compression
- Icecast and Shoutcast streaming support
- Library synchronization with disk

---

![P-Layer Screenshot](screen1.png)

![P-Layer Screenshot](screen2.png)

![P-Layer Screenshot](screen3.png)

---

# 1. Quick Start

Before using the application, open **Settings** from the left sidebar.

---

# 2. Settings

## General

### Playlist Folder

Folder where scheduled playlists (.m3u) are stored.

Used by the **Scheduler** module.

### Crossfade Duration

Used only if a track does not contain a **Fade Out marker**.

### Smart Crossfade

Automatic silence detection settings:

- Silence Threshold
- Silence Window
- Only in last (sec)

### Compressor Mode

- Off
- Soft
- Punchy (recommended for broadcast sound)

---

## Categories (Required)

At least one category must be created for the Library to function.

To create a category:

1. Enter Category Name
2. Choose Color
3. Select Folder with audio files
4. Confirm ✔

All files from the selected folder will appear in the **Library**.

Recommended structure:

```
Music/
  Rock/
  Pop/
  Dance/
  VoiceTracks/
```

---

# 3. Rotator (Music Rotation)

The **Rotator** module generates broadcast playlists based on hourly clock templates.

It consists of several components.

### Clock Editor

Editor for hour templates.

Each hour contains category positions, for example:

```
MUSIC A
MUSIC B
MUSIC C
JINGLE
MUSIC A
```

### Clock Wheel

Visual representation of the hour template.

Allows quick understanding of the hour structure.

### Categories

Categories serve as music sources for the rotator.

### Schedule

Assigns clock templates to specific hours of the day.

---

## Playlist Generation

Rotator can automatically generate **daily playlists (.m3u)**.

Process:

1. A schedule of clocks is created
2. Rotator selects tracks from categories
3. Separation rules are applied
4. A playlist is generated

---

## Rotation Rules

Supported rules:

### Artist Separation

Limits how frequently the same artist can appear within a rotation.

### Track Separation

Prevents the same track from repeating too often.

These rules ensure professional radio-style music rotation.

---

# 4. Voice Tracking

**Voice Tracking allows voice segments to be played over music tracks, using the intro or transition between songs.**

To use Voice Tracking:

Enable the option in the category settings:

```
Use for Voice Tracking
```

Any track placed in such a category will be treated as a **Voice Track (VT)**.

---

## Playback Logic

When a Voice Track is placed between two music tracks:

### Case 1

If the next track has an **Intro marker** and the intro duration is greater than or equal to the Voice Track length:

The Voice Track plays entirely inside the next track's intro.

### Case 2

If the intro is shorter than the Voice Track:

The Voice Track starts on the tail of the previous track  
and ends exactly at the end of the next track's intro.

### Case 3

If the next track has no intro marker:

The Voice Track starts on the tail of the previous track  
and ends exactly at the beginning (0 point) of the next track.

All timing is calculated using **playback counters**.

No artificial delays are used.

---

## Ducking

During Voice Track playback, music volume is automatically reduced.

After the voice segment ends, the volume returns to normal.

Configurable parameters:

- Ducking Amount
- Release Time

---

# 5. Library & Playlist

## Library

The right panel contains:

- **Files** — categorized audio files
- **Commands** — automation commands

Real-time search is available.

---

## Playlist Management

- Drag tracks from the Library or Finder
- Reorder using drag & drop
- Remove tracks using ✖
- **Clear Playlist** removes all items

Tracks added directly from Finder appear uncategorized unless matched by folder rules.

---

# 6. Track Markers

Markers are edited in the **Track Editor**.

---

## Intro Marker

Defines the end of the intro section.

Used for:

- intro countdown display
- Voice Tracking timing

---

## Fade Out Marker

Defines the transition point.

The next track starts exactly at this moment.

If Fade Out is set:

- global Crossfade is ignored
- transition occurs strictly at the marker

---

# 7. Automation Commands

Playlists can contain zero-duration commands:

- Start Stream
- Stop Stream

Commands execute instantly while playback continues.

Commands are stored directly inside **.m3u** playlists.

---

# 8. Scheduler

The Scheduler checks for scheduled playlists every **10 seconds**.

---

## Playlist Format

```
YYYY-MM-DD_HH-MM.m3u
```

When system time matches the file name, the playlist loads automatically.

---

## Behavior

If playback is already running:

the playlist switches seamlessly.

If playback is stopped:

the playlist loads and starts automatically.

---

# 9. On-Air Control

Main controls:

- Play
- Pause
- Next
- Eject

The **STREAM** button controls broadcasting.

States:

- OFF
- CONNECTING
- ON
- ERROR

---

# 10. Technical Specifications

Supported formats:

- MP3
- WAV
- FLAC
- M4A

Recommended sample rate:

```
44.1 kHz
```

If a file has an incorrect sample rate, a warning ⚠️ is displayed.
