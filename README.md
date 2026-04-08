# P-Layer

P-Layer is a professional broadcast automation application designed for radio stations, community radio, and streamers. It provides precise playlist control, audio processing, scheduling, streaming (Icecast/Shoutcast), and integrated Voice Tracking.

![P-Layer Screenshot](screen1.png)

![P-Layer Screenshot](screen2.png)

![P-Layer Screenshot](screen3.png)
---

## 1. What This App Does

P-Layer allows you to:

1. Run live playback from a queue (Studio).
2. Store and edit a categorized music library.
3. Mark up tracks in Audio Editor (Start / Intro / Fade Out).
4. Auto-load playlists by time.
5. Generate playlists in Rotator (PRO).
6. Edit existing playlists or create playlists manually, including adding/removing items.
7. Plan ad/service break filling in Planner (PRO).
8. Start/stop stream output (Icecast/Shoutcast) manually or by playlist commands.
9. Record voice tracks and save them to library or directly into playlist (PRO).
10. Play voice tracks over music tracks with automatic positioning on intro or at track end.

---

## 2. Main Windows and Buttons

### Main Window (Studio)

Left sidebar:

1. `Library`
2. `Rotator`
3. `Planner`
4. `Playlist`
5. `Settings`
6. `VT Recorder`

Top center:

1. Player controls (`Play`, `Pause`, `Next`, `Eject`)
2. `STREAM OFF/ON` button

Below:

1. Queue (track cards)
2. Queue toolbar buttons:
   - `Compact view`
   - `Open audio`
   - `Open folder`
   - `Save playlist`
   - `Load playlist`
   - `Clear queue`

Right side:

1. Library (`Tracks` / `Commands`)
2. Library search

---

## 3. First Launch: Setup Before Going On Air

## Step 1. Select Playlist Folder

1. Click `Settings` in the left sidebar.
2. Open the `General` tab.
3. In `Playlist Folder`, click `Select Folder`.
4. Choose your working `.m3u` folder.

Result:

1. This folder will be used for:
   - `Save playlist`
   - `Load playlist`
   - auto-loading scheduled playlists
   - Rotator generated files.

## Step 2. Create Categories

1. In `Settings`, open `Categories`.
2. In `Add New Category`, fill:
   - `Category Name`
   - color
   - `Category Path` via `Select Folder` (recommended)
3. Optional flags:
   - `Play Over` for voice tracks
   - `Non Music` for ad/news/service categories used in Planner.
4. Click `Add`.

Result:

1. Category appears in categories list.
2. Tracks from that folder appear in Library.

## Step 3. Configure Audio Outputs

1. In `Settings -> General`, find `Audio Output Routing`.
2. Set:
   - `Program Output Device` (main on-air output)
   - `Preview Output Device` (Audio Editor preview output)

Result:

1. Studio player uses Program output.
2. Audio Editor uses Preview output.
3. If Preview is not selected or disappears, preview falls back to Program output.

## Step 4. Configure Streaming (if needed)

1. `Settings -> Streaming`.
2. Enable `Enable streaming`.
3. Fill:
   - `Server type`
   - `Host`
   - `Port`
   - `Mountpoint / Stream ID`
   - `Username`
   - `Password`
   - `Bitrate`

Result:

1. `STREAM` button in Studio can start real stream output.

## Step 5. Exit Settings

1. Click `Back` at the bottom of the settings view (above Support block).

Result:

1. You return to the main Studio screen.

---

## 4. Working with Library

## Where to View Tracks

1. Right panel `Library`.
2. `Tracks` tab: audio tracks by categories.
3. `Commands` tab: `Start Stream` and `Stop Stream`.

## What You Can Do in Library

1. Drag tracks into queue.
2. Double-click a library track to open Audio Editor.
3. Right-click a track -> `Edit Markers`.
4. Use `Search`.

## Library Hints

1. If artist is empty or title looks like raw filename with extension, row is dimmed.
2. `⚠️` icon means non-standard sample rate (not 44.1 kHz).

---

## 5. Studio Queue: Basic Workflow

## Add Tracks

1. Drag tracks from `Library -> Tracks` into queue.
2. Or click `Open audio` and select a file.
3. Or click `Open folder` to add all supported files from a folder.

Supported formats: `mp3`, `wav`, `flac`, `m4a` (drag&drop also supports `ogg`).

## Reorder

1. Drag queue cards to new positions.

## Remove

1. `x` on card removes one item.
2. `Clear queue` clears entire queue.

## Compact View

1. Click `Compact view` to toggle compact queue cards.

## Edit Track from Queue

1. Double-click track card -> Audio Editor.
2. Or right-click -> `Edit Markers`.

Result:

1. After `Save` in Audio Editor, queue card updates marker/title data without full queue rerender.

---

## 6. Audio Editor: How to Mark a Track

## How to Open

1. From queue: double-click track card.
2. From library: double-click track row.
3. From context menu: `Edit Markers`.

## Marker Meanings

1. `Start` — playback start point inside file.
2. `Intro` — intro end point.
3. `Fade Out` — exact point where next track should start.

## Basic Marking Scenario

1. Start playback with `Play`.
2. At required position, click `Start`.
3. At intro end, click `Intro`.
4. At transition point, click `Fade`.
5. Fine-adjust with `←/→` (50 ms step).
6. Click `Save`.

Result:

1. Markers are saved to library DB.
2. Audio Editor closes automatically after successful `Save`.
3. Queue/now-playing data in Studio is updated.

## Useful Buttons

1. `Undo`
2. `Zoom -> Start`
3. `Show Full`
4. `Zoom -> End`
5. `Zoom` slider
6. Spacebar starts playback.

## Crossfade and Intelligent Crossfade (Settings -> General)

`Crossfade (sec)`:

1. This is the overlap duration between two tracks.
2. In P-Layer, the next track does not fade in; it starts instantly at full level at transition time.
3. When the second track starts, the first track begins fading out.
4. `Crossfade` defines how long this tail fade-out lasts.

In other words:

1. The second track starts instantly.
2. The first track fades out.
3. Fade-out duration equals `Crossfade`.

`Intelligent Crossfade` is used when a track has no `Fade Out` marker.

Parameters:

1. `Silence threshold (0.00–0.20)` — signal level threshold; anything below it is treated as silence.
2. `Silence window (ms)` — minimum silence duration to be considered valid (very short dips are ignored).
3. `Smart crossfade only in last (sec)` — limits analysis to the last N seconds, so quiet mid-song parts do not trigger early transitions.

Logic:

1. If suitable silence is found, the next track starts at that point.
2. If no silence is found, the system falls back to regular `Crossfade (sec)`.

---

## 7. On-Air Playback and Streaming

## Player Controls

1. `Play` — start queue playback.
2. `Pause` — pause.
3. `Next` — skip to next queue item.
4. `Eject` — stop/reset playback.

## Streaming Control

1. `STREAM OFF` button:
   - click -> connect to server
   - statuses: `CONNECTING`, `STREAM ON`, `STREAM ERROR`, `STREAM OFF`

Important:

1. If `Enable streaming` is disabled in `Settings -> Streaming`, button shows `DISABLED`.

## Playlist Commands

1. In `Library -> Commands`, available:
   - `Start Stream`
   - `Stop Stream`
2. Drag these commands into queue/playlist.

Result:

1. During playback, command executes automatically.

## System Now Playing (macOS)

1. During playback, P-Layer publishes current track metadata to macOS system media:
   - `title`
   - `artist`
   - `album` (if present)
   - duration and current position
2. This is needed for integration with macOS-aware apps (for example Audio Hijack), so they can detect the current track and progress automatically.
3. On full playback stop (`Eject`/stop), system now-playing state is cleared.

## External Now Playing Metadata Files

1. On confirmed start of a music track, P-Layer updates:
   - `~/Music/P-Layer/nowplaying.json`
   - `~/Music/P-Layer/CurrentPlaying.txt`
2. This is needed for external integrations that read metadata from files: OBS overlays, broadcast automation, and custom scripts.
3. While break-session items are playing, these files are not overwritten; the last music track remains.
4. Formats:
   - `nowplaying.json`
     ```json
     {
       "artist": "...",
       "title": "...",
       "started_at": "ISO timestamp"
     }
     ```
   - `CurrentPlaying.txt`
     ```text
     Artist - Title
     ```

---

## 8. Save/Load Playlists and Time-Based Auto-Load

## Manual Save

1. In Studio click `Save playlist`.
2. Save `.m3u` file to desired folder.

## Manual Load

1. Click `Load playlist`.
2. Select `.m3u`.

Result:

1. If playback is active, load is seamless (transition to new playlist).
2. If stopped, playlist loads and starts playback immediately.

## Auto-Load by Time (Scheduler)

How it works:

1. App checks every 10 seconds for a file matching current minute.
2. Filename format must be exact: `YYYY-MM-DD_HH-MM.m3u`.
3. If you do not want auto-load, do not use this date/time mask in the filename.
4. You can name playlist files any other way (`.m3u` not matching this mask), and they will not auto-start.

Example:

1. `2026-03-28_14-30.m3u`

Result:

1. At `14:30` this playlist auto-loads.

---

## 9. Playlist Editor (Separate Window)

## How to Open

1. Click `Playlist` in Studio left menu.
2. Or double-click row in `Rotator -> Schedule -> Generated Playlists`.

## What You Can Do

1. Build playlist via drag&drop from Library.
2. Reorder items.
3. Add `Start/Stop Stream` commands.
4. See total time and cumulative card timing.
5. Use `Load playlist`, `Save playlist`, `Clear playlist`.
6. Use `Compact view`.
7. Record voice tracks into playlist. Select a track and click `VT Recorder`.

## Break Marker Behavior

1. If playlist contains `[BREAK:N]`, it is shown as `Break N` card.
2. Break card is visible but not editable as regular track (does not open Track Editor).
3. Drag-reorder and delete are still available.

---

## 10. Rotator (Schedule Generator)

Open with `Rotator` button in Studio.

Rotator has 3 tabs:

1. `Clock Editor`
2. `Categories`
3. `Schedule`

## 10.1 Clock Editor

Goal:

1. Build hour template (clock) from categories and break markers.
2. Add repeating elements such as jingles.

How to create a clock:

1. Enter name in `CLOCK NAME`.
2. Drag categories from right `CATEGORIES` panel into `CLOCK SLOTS`.
3. Add break slots from `BREAKS` panel if needed.
4. Reorder slots with drag&drop.
5. Click `Save`.

Result:

1. Clock is saved and available in Schedule generation.

Extra actions:

1. `New` — new unsaved draft.
2. `Delete` — delete selected clock.
3. In `BREAKS`, you can set custom names for Break1..Break5.

## 10.2 Categories

This tab sets rotation rules:

1. Per category: `TRACK SEPARATION MIN`.
2. Global: `ARTIST SEPARATION (MIN)`.

If set to `0`, restriction is disabled.

## 10.3 Schedule

Goal:

1. Generate `.m3u` files into playlist folder.

Steps:

1. Select `CLOCK TEMPLATE`.
2. Select `DATE`.
3. Select `HOURS` mode:
   - `All 24 hours`
   - `Selected hours`
   - `Standalone playlist`
4. Click `Generate`.

Result:

1. Files appear in `Generated Playlists`.
2. `Last Generation Details` shows warnings/details.

In `Generated Playlists`:

1. Double-click row -> open file in Playlist Editor.
2. Click `x` in row -> delete file from disk.

## PRO in Rotator

Rotator generation requires PRO.

Activation:

1. Open `Help -> Copy License Request Code`.
2. Send the code to support and receive a `LICENSE KEY`.
3. Open `Help -> Activate License…`.
4. Paste your key into `LICENSE KEY` and click `Activate`.
5. Verify status via `Help -> License Status…`.

---

## 11. Planner (Break Planning)

Open with `Planner` button in Studio.

Planner is available in free version, but break content fill in runtime playback requires PRO.

## Planner Layout

Left side:

1. `Planner Grid` (Break1..Break5 x 24 hours)
2. `Break Editor` (selected slot content)

Right side:

1. Library filtered to categories with `Non Music` flag.

## How to Fill a Slot

1. Select date (`Date`, `Today`, `Copy Prev Day`).
2. Click a track in right library (it becomes selected).
3. Click target cell in grid (hour + break).

Result:

1. Track is added to that slot.
2. Item appears in `Break Editor -> Planned Items`.

## Change Order Inside Slot

1. In `Break Editor`, use:
   - `↑`
   - `↓`

Result:

1. Order is saved in DB and used in break playback.

## Remove Items

1. `x` next to item to remove one.
2. `Clear Slot` to remove all items from selected slot.

## Day Actions

1. `Copy Prev Day` — copy full previous day plan to selected date.
2. `Clear Day` — clear all slots for selected date.

## PRO in Planner

Activation flow is the same as Rotator:

1. Open `Help -> Copy License Request Code`.
2. Send the code to support and receive a `LICENSE KEY`.
3. Open `Help -> Activate License…`.
4. Paste the key and click `Activate`.

After activation, break cards in Studio refresh without app restart.

---

## 12. Break Markers in Playlist and Playback

Marker format:

1. `[BREAK:N]`, where `N = 1..5`.

Where markers come from:

1. Rotator inserts markers into generated playlists.
2. Studio and Playlist Editor parse them safely as break items (not file paths).

## How It Looks in Studio

Queue shows dedicated break card:

1. `Break N`
2. subtitle `Planner block` or `PRO license required to fill break`
3. spot count
4. total duration

## Playback Logic

1. Empty break -> skipped.
2. Non-empty break -> plays items planned in Planner for:
   - current date
   - current hour
   - matching BreakN.

Important:

1. Smart silence-based crossfade is not applied to tracks played inside break sessions.

---

## 13. Voice Track (Play Over)

How to enable:

1. `Settings -> Categories`.
2. Enable `Play Over` flag on desired category.

What this gives:

1. Tracks in this category become voice tracks.
2. You can attach them to music cards.

How the system knows a track has an intro:

1. Intro must be marked in advance in `Audio Editor`.
2. Put `Intro` marker at the point where instrumental intro ends and vocals begin.
3. If `Intro` is not marked, the track is treated as having no intro.

How to attach voice track manually:

1. Take voice track from `Library`.
2. Drag it onto a music track card and release.
3. This works both in Studio queue and in `Playlist Editor`.

Result:

1. Card shows `🎤` badge.
2. Voice track plays over the intro.
3. Voice track ends exactly at the point where vocals begin (`Intro` marker).

How to detach:

1. Click `✖` in voice badge on card.

Automatic voice track rotation:

1. Create a separate folder on disk for voice tracks.
2. Put prepared voice tracks into that folder.
3. Connect this folder in `Settings -> Categories` as `Category Path` for your voice category.
4. Enable `Play Over` for that category.
5. Tracks from this category can then be used for regular voice break rotation during the hour.

## 13.1 VT Recorder (VoiceTrack Studio): Record Your Own Voice Track

## How to Open

1. In main Studio window: `Tools -> VT Recorder` (left sidebar).
2. In Playlist Editor: `Tools -> VT Recorder`.

Result:

1. `VoiceTrack Recorder` window opens.
2. If a music track was selected before opening, the top `Attach To` block shows:
   - full track title (`Artist - Title`);
   - `Intro` value (if set).

## Prepare Before Recording

1. In `Name`, enter voice track name (or leave empty).
2. In `Input`, select microphone.
3. Watch vertical `Input Level` meter on the right:
   - it works before recording starts;
   - `CLIP` means overload.

## Record

1. Click `RECORD` (or press `R`).
2. Speak into microphone while monitoring `Input Level`.
3. Click `STOP` (or press `R` again).

Result:

1. Recording is prepared automatically before save (start/end trim, level normalization, peak limiting).

## Preview and Delete

1. `PLAY` — preview recorded result.
2. `DELETE` — remove current recording and start again.

Important:

1. Preview output uses `Preview Output Device` from `Settings -> General`.
2. If preview device is unavailable, playback falls back to `Program Output Device`.

## Save (SAVE)

1. Click `SAVE` — no system save dialog is shown.
2. File is saved automatically into category folder marked as `Play Over` (Voice Over).
3. File name is taken from `Name`:
   - if empty: `VT_1.wav`, then `VT_2.wav`, `VT_3.wav`, etc.;
   - if provided: `name.wav`, then `name_2.wav`, `name_3.wav`, etc.
4. Saved file format: `PCM WAV`, `44.1 kHz`, `16-bit`, `mono`.

## Attach to Selected Track

1. If VT Recorder was opened with a selected music track (from Studio or Playlist Editor), after `SAVE` the voice track:
   - is saved into Voice Over folder;
   - is automatically attached to that selected track (same behavior as drag&drop).
2. If no track was selected (or track was removed), only file save is performed.

## License (PRO)

1. Without PRO you can:
   - open VT Recorder;
   - record;
   - preview;
   - delete recording.
2. `SAVE` is PRO-only.
3. Without PRO, `SAVE` shows informational modal:
   - `Saving Voice Tracks is available in the PRO version.`
4. License activation:
   - `Help -> Copy License Request Code`;
   - send the code to support and receive a key;
   - `Help -> Activate License…` -> paste key -> `Activate`;
   - check status: `Help -> License Status…`.

---

## 14. Practical Scenario: Prepare a Broadcast Day

1. In `Settings`, verify `Playlist Folder`, `Streaming`, audio outputs.
2. In `Rotator -> Clock Editor`, build/review clock template.
3. In `Rotator -> Categories`, set separation rules.
4. In `Rotator -> Schedule`, generate playlists for target date.
5. In `Planner`, fill required break slots for that date.
6. In VT Recorder, record voice tracks and add them to playlist.
7. In Studio, load specific file manually (`Load playlist`) if needed, or rely on scheduled auto-load.
8. Before going live, switch `STREAM` on.

---

## 15. Common Issues and Quick Fixes

## Playlist Did Not Auto-Load

Check:

1. `Settings -> General` has correct `Playlist Folder`.
2. Filename is exact `YYYY-MM-DD_HH-MM.m3u`.
3. System time is correct.

Important:

1. Files not matching `YYYY-MM-DD_HH-MM.m3u` are never auto-loaded and can only be started manually via `Load playlist`.

## Planner Right Panel Has No Tracks

Reason:

1. No categories with `Non Music` enabled.

Fix:

1. Enable `Non Music` on required categories in `Settings -> Categories`.

## Break Card Shows “PRO license required to fill break”

Reason:

1. PRO is not activated.

Fix:

1. Activate PRO via `Help -> Activate License…`.
2. If you do not have a key yet: use `Help -> Copy License Request Code`, send it to support, and receive a key.

## Rotator Generation Fails

Check:

1. PRO license is active.
2. Clock template is selected.
3. Date is selected.
4. In `Selected hours` mode, at least one hour is selected.
5. `Playlist Folder` is configured.

## Double-Click on Generated Playlist Does Not Open

Reason:

1. File was deleted outside the app.

Fix:

1. Refresh list (focus Rotator window again, or generate again).
2. Re-generate missing file.

---

## 16. Pre-Broadcast Checklist

1. `Settings -> General`: Program output verified.
2. `Settings -> Streaming`: `Enable streaming` on, credentials filled.
3. `Rotator` (if used): schedules for target date are generated.
4. `Planner` (if breaks used): break slots are filled.
5. In Studio, correct queue/playlist is loaded.
6. `Play` starts successfully.
7. `STREAM` status is `ON`.
