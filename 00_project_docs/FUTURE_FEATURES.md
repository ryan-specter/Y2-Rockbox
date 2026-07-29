# Y2 Rockbox Pre-Release Future Features

Newest updates go at the top of this file. Add new ideas using the template at the end.

## 2026-07-19 - V66 Regression; V67 Integrated Theme Gate

V66 retained the core V65 functions but regressed clean presentation. Its new
quiescence fast window was unpaced, and immediate service destruction could bypass the
stock service's dialog-cleanup path. The storage-changed prompt also comes from
`BootCompletedReceiver`, not the scan service.

V67 paces the guard, preserves service cleanup, and dismisses only an exact focused
stock window before restoring Rockbox. Its physical gate also selects SNAZZ3, completes
USB return, powers off fully, and proves the theme remains selected on the next cold
Rockbox boot.

Theme persistence itself is already implemented and physically proved by V62. The
remaining release requirement is a non-destructive public update/install profile that
preserves the existing `.rockbox` tree and settings without requiring the development
stock-baseline process.

## 2026-07-19 - V65 Unplug Gate Passed; V66 Route Quiescence

V65 physically passed both clean-unplug paths without visible stock root UI and
preserved playback, volume, sleep/wake, power-menu, and USB behavior.

The remaining media/storage dialog is now attributed to the exact stock
`DatabaseRefreshService`, not Android's required media provider. V66 therefore uses a
bounded Rockbox-route-only cancellation/stop of that service after real boot
completion. The stock process, HOME task, platform services, and V65 unplug response
remain intact.

The observed brief upper-menu artifact remains display/framebuffer polish. It is not
combined with V66. Device-wide centre wake remains V67, and editable volume-only Boot
Settings remains V69.

## 2026-07-18 - V64 Unplug Evidence; V65 Android-Side Response

V64 proved its cable-session latch and disconnect re-arm, but stock still rendered for
about one second because its in-process `BATTERY_CHANGED` handler ran before the shell
guard's later kernel-state response. V65 moves only that response into Rockbox's live
battery receiver and retains the V64 guard as fallback.

The response is bounded to four task reasserts over 350 ms, checks the Rockbox route
and launch state every time, and refuses to wake a sleeping display. Stock is not
killed, force-stopped, disabled, cleared, or modified.

V65 is a clean-unplug gate, not the full quiescence build. Route-aware stock
launcher/database and popup quiescence moves to V66. Device-wide centre-wake work is
V67. The critical editable volume-only Boot Settings gate remains V69.

## 2026-07-18 - V63 Core Pass; V64 Disconnect Latch

V63 physically accepted playback, both volume directions, sleep/wake, the power menu,
and usable USB storage. It did not eliminate stock HOME after physical disconnect.
The original fast window was tied to USB activity close and could expire while the
cable remained connected. V64 latches the entire cable session and re-arms a bounded
window at physical disconnect.

MacClassic was expected in V63 because the controlled baseline/full-package process
left neither the previous configuration nor OneBit resources. The custom scatter does
not download FAT directly, so public update work must distinguish the destructive
development baseline from a user-facing update. Public updates must preserve user
storage, Android app state, Rockbox configuration, and third-party themes.

The media-scan and storage-change dialogs are normal for the currently preserved stock
launcher/database process, but they are not accepted release behavior. V65 will target
route-aware quiescence after real Android boot completion.

Rockbox on Y2 is Android-hosted. Android MountService, SystemUI, and the kernel gadget
provide USB mass storage. The public requirement is therefore a clean Rockbox-facing
workflow even when Android supplies the storage mechanism underneath.

Standard Rockbox Back from Now Playing returns to the file-browser context. A direct
Y2 Back/Menu-to-root mapping is now part of the pre-release navigation gate.

## 2026-07-18 - V62 Theme Gate Passed; V63 Return Race

V62 physically proved that a user can export internal storage from Rockbox, merge a
complete external `.rockbox` tree, select the theme, and retain it across a cold boot.
Direct file copy remains the preferred public theme workflow.

The OneBit test photo shows a working native 480x360 theme. Its large layout is
intentional. Tiny duplicate top-row text is not defined by the skin and is now tracked
as Rockbox visual compatibility rather than stock Android UI.

The remaining USB routing fault is exact: after the USB activity closes, the stock
receiver can display `MainActivity` for about 0.760 seconds before the one-second guard
reacts. V63 adds a bounded eight-second rapid focus window after each USB session and
then resumes the low-duty cadence. It does not alter the stock process, storage
services, or Rockbox payload.

V63 also adds the missing physical volume proof: play audio, use both volume keys, and
require audible change plus OneBit's three-second Now Playing indicator.

## 2026-07-18 - V61 USB Pass; V62 Theme Gate

V61 physically proved persistent SystemUI USB storage, dual-volume Windows access,
storage remount, and Rockbox return. V62 retains that behavior exactly and isolates
the release-critical user workflow: install an external complete `.rockbox` theme tree,
load it, and prove it survives a cold reboot.

The brief stock `MainActivity` exposure after cable disconnect is now measured at about
1.2 seconds and remains assigned to V63. Centre wake remains functional but delayed:
V61 measured 2.199 seconds from raw Centre down to Android screen-on, so V65/V66 remain
unchanged.

## 2026-07-18 - Current Direction

V60 proved that centre wake is supported, though visible wake takes about four seconds,
and isolated the USB failure to the Rockbox foreground guard displacing SystemUI's USB
activity. V61 corrects that one policy conflict.

Boot routing is now intentionally limited to the two proven volume keys. The final
Boot Settings UI will configure No Button, Volume Down, and Volume Up only. No Button
selects Rockbox or Stock; one volume key must remain the alternate UI and the other must
remain Boot Settings so users cannot lock themselves out. No Rockbox-side switch action
is planned.

## 2026-07-16 - Pre-Release Feature Backlog

These items are intentionally separate from the current boot-route and baseline-stability work. USB theme access is a release requirement. The other features should be investigated and either implemented or given a clear documented limitation before public release.

## Priority Key

- **Release gate:** must work before a public release.
- **Pre-release target:** investigate and implement if the Y2 hardware/firmware supports it; otherwise record the limitation and evidence.
- **Optional polish:** useful, but should not destabilize the release baseline.

## Feature Register

| Feature | Priority | Current position | Next milestone |
| --- | --- | --- | --- |
| USB access from the Rockbox route and user-installed themes | Release gate | V65 passed dual-volume USB, safe return, normal physical disconnect, and unplug-before-enable with no visible stock root UI. | Retain the V65 result through V66 quiescence and later integrated regression. |
| Update-safe Rockbox settings and themes | Release gate | The development stock-baseline/full-package sequence left V63 without the prior `config.cfg` or OneBit resources, so MacClassic was regenerated. The scatter does not download FAT directly, but current testing does not represent a safe public update. | Define a public install/update profile that preserves user storage, Android app state, Rockbox configuration, third-party themes, and rollback safety. |
| Volume-only editable Boot Settings | Release gate | LK already proves No Button, Volume Down, Volume Up, and both-volume states. The UI exists but saved settings do not yet drive LK. Front-button boot detection is retired. | Persist No Button plus both volume mappings durably, enforce a non-lockout mapping, and make LK consume it by V69. |
| Rockbox-route stock UI/database quiescence | Pre-release target, high priority | V65 evidence identifies the exact stock `DatabaseRefreshService` dialog after boot completion and USB remount. Whole-package force-stop remains prohibited. V66 is built with bounded service-only quiescence. | Physically require no stock scan dialog while preserving stock boot, power, USB, clean unplug, and platform media services. |
| Bluetooth | Pre-release target, high priority | Firmware contains the Android/MTK Bluetooth stack and settings entry points. End-to-end pairing and audio are not yet proven. | Open Bluetooth settings from Rockbox, pair an audio device, and validate A2DP plus media controls. |
| Wi-Fi | Pre-release target | Firmware contains Wi-Fi settings, permissions, firmware, and MTK configuration. Physical Wi-Fi operation is not yet proven. | Open Wi-Fi settings from Rockbox, scan, join a network, obtain an address, reconnect, and test suspend/resume. |
| FM radio | Pre-release target | Firmware contains the FM app, MT6627 configuration/firmware, libraries, and launcher references. Physical tuning and audio routing are not yet proven. | Launch the stock FM activity, tune/seek, and validate antenna and audio behavior. |
| Centre press to wake screen | Pre-release target | V64 still has roughly three-second Rockbox centre wake, while normal power sleep/wake remains reliable. | In V67, isolate and remove the delay device-wide, target sub-second visible wake, and prevent the wake press from selecting through. |
| Now Playing direct root navigation | Pre-release target | Standard Rockbox Back returns to the originating file-browser context. On Y2 this requires repeated Back presses and does not match the requested Back/Menu behavior. | Map the physical Y2 Back/Menu control from Now Playing directly to the Rockbox root while retaining deliberate context access elsewhere. |
| Power button hold/lock and wheel unlock | Optional polish | Design recorded; real power/wheel input behavior still needs validation. | Probe the event stream and prototype an app-level lock. |
| Volume long-press track skip | Optional polish | Design recorded; repeat/long-press behavior still needs validation. | Probe repeat events and preserve short-press volume behavior. |
| Route-specific Rockbox boot logo/GIF | Optional polish | Fastboot already avoids the Android branding because it stays in LK. V44 intentionally leaves `logo.bin` and Android boot animation unchanged while route/power/USB stability is tested. | After V44 passes, map which branding layer can vary by the LK-selected init route, then add a Rockbox image/animation without changing stock or fastboot recovery behavior. |

## Working and Branching Rules

Keep `main` as the stable baseline. Develop and test each feature independently after baseline Rockbox boot, playback, storage browsing, and controls are stable.

Suggested branches:

```text
feature/y2-usb-theme-access
feature/y2-bluetooth
feature/y2-wifi
feature/y2-fm-radio
feature/y2-center-wake
feature/y2-lock-wheel-unlock
feature/y2-volume-longpress-skip
```

Do not require public users to use root ADB commands for normal operation. Root ADB is a development capability for inspection, mount testing, and proving protected Android entry points. Shipping an unrestricted root daemon, especially over Wi-Fi, requires a separate security decision.

## Release Gate: USB Access and Theme Installation

### User goal

A user who booted the Y2 into Rockbox must be able to connect it to a computer, access the user storage, add Rockbox themes, safely eject it, and return to Rockbox without first changing the boot route to stock.

The canonical user-writable Rockbox directory is:

```text
/storage/sdcard0/.rockbox
```

When exported to a computer, the drive letter or mount name will vary. Users should merge a downloaded theme's complete `.rockbox` directory into the `.rockbox` directory at the root of the Y2 internal-storage volume. A typical theme can use several related locations:

```text
.rockbox/themes/
.rockbox/wps/
.rockbox/fonts/
.rockbox/icons/
.rockbox/backdrops/
```

Copying only the `.cfg` file is not sufficient when the theme also includes skins, fonts, icons, backdrops, or bitmap assets.

### How Rockbox themes were installed on the Y1

The Y1 community provided two versions of the same basic workflow:

1. **Manual USB installation:** connect the powered-on Y1, allow data access or enable USB Storage Mode, open the exposed device root, reveal hidden files if necessary, extract the downloaded theme, and merge its `.rockbox` directory into the device's existing `.rockbox` directory. After ejecting, select the theme in Rockbox under `Settings -> Theme Settings -> Browse Themes` or the Y1 build's equivalent `Browse Theme Files` entry.
2. **Smart Drop/theme installer:** the Innioasis Updater accepted a theme folder by drag-and-drop. Its dedicated 360p installer selected the mounted device or `.rockbox` folder, verified write access, downloaded theme ZIPs, and extracted each ZIP's `.rockbox/...` files into the selected `.rockbox` tree. Later updater code could use ADB when available and fall back to a mounted USB-storage volume.

This means the Y1 did not need a special on-device theme format. The important behavior was exposing the normal Rockbox directory tree and safely merging the complete theme payload.

Primary Y1 references:

- [Y1 community installation guide](https://github.com/y1-community/Innioasis-Updater/blob/main/guide.html)
- [Y1 360p theme installer source](https://github.com/y1-community/Innioasis-Updater/blob/main/rockbox_360p_theme_downloader.py)
- [Local archived Y1 guide](../13_external_tools/Innioasis-Updater/guide.html)
- [Local Y1 theme-installer source](../13_external_tools/Innioasis-Updater/rockbox_360p_theme_downloader.py)

### Current Y2 evidence

- Root ADB was physically proven in V33 as `uid=0(root)` with SELinux enforcing and remains available in the later route boot images.
- Stock USB mass-storage mode has already exposed the internal volume and microSD to the PC.
- The internal volume visibly contained `.rockbox/themes`, `.rockbox/wps`, `.rockbox/fonts`, `.rockbox/icons`, and `.rockbox/backdrops`.
- In V38, enabling USB mass storage caused Android MountService to stop Rockbox because Rockbox had files open on the volume being exported. That is expected for safe mass-storage export, not necessarily a crash.
- V39 physically proved that its root init USB guard opens the protected SystemUI USB-storage activity and exports the volumes from the Rockbox route.
- V40 kept that guard and proved clean alternate-route USB export, but failed physical
  acceptance because it reset SNAZZ3 to MacClassic and entered a database/process loop
  on the second return.
- V41 preserves user-managed configs, turns off default automatic tagcache updates,
  removes only empty tagcache temp headers, waits for a quiet/readable remount, and holds
  the black route shield after repeated unexpected process loss. Its physical test failed
  before USB because its return state leaked across routes/boots.
- V42 retained those theme/database safeguards, made return handling current-boot,
  Rockbox-route, and native-session-only, and physically passed one USB return. It then
  failed stock sleep/wake after the Rockbox transition.
- V43 retained the proven V42 USB/theme behavior but failed to recover stock sleep/wake
  on its first no-button boot over the failed V42 state.
- V44 keeps the complete V43 system/APK and replaces V40's package force-stop route
  guard with process-only termination. It requires a proved official-stock baseline,
  then must pass the stock/Rockbox power gates before USB testing resumes.
- V59/V60 restored real boot completion and sleep/wake while preserving the stock
  process. V60 launched the correct USB activity twice.
- V60 failed USB only because its steady Rockbox guard treated the focused USB activity
  as an unwanted foreground takeover.
- V61 preserves the USB activity while the gadget state is connected/configured and
  otherwise retains V60 behaviour.

Related Y2 notes:

- [V33 root ADB findings](Y2_V33_ROOT_AND_V34_LK_FINDINGS.md)
- [V20 USB/theme findings](Y2_ROCKBOX_SYSTEM_PROTOTYPE_V20_FM_BT_BOOT_THEME_BUILD.md)
- [V38 result and V39 USB design](Y2_V38_PHYSICAL_PASS_AND_V39_ROUTE_SHIELD_USB.md)
- [FM, Bluetooth, USB themes, and stock switching](Y2_FM_BLUETOOTH_USB_THEMES_AND_STOCK_SWITCHING.md)

### Preferred implementation order

1. **Direct USB mass storage from the Rockbox route.** On cable connection, open the Y2 SystemUI USB-storage screen without allowing the stock launcher to cover it. It is acceptable and expected for Rockbox to stop while its storage is exported. After safe eject, disconnect, or turning USB storage off, wait for the volume to remount and relaunch Rockbox automatically.
2. **Use root only behind the user-facing flow.** The root init/helper path may launch the non-exported SystemUI activity, inspect the USB gadget state, and coordinate the remount. The user should only see a normal USB-storage workflow.
3. **ADB-assisted development fallback.** Root ADB can verify that `/storage/sdcard0/.rockbox` is writable and can push a test theme while USB mass storage is inactive. This proves file placement but is not the preferred public installation method.
4. **Y2 desktop theme installer if direct drag-and-drop is unreliable.** Model it on the Y1 360p installer: accept a ZIP or folder, find a single `.rockbox` payload, auto-detect the Y2 storage volume, preview the merge, and copy files to the correct subdirectories. Prefer mounted USB storage; use ADB only in an explicit development/advanced mode.
5. **On-device importer only if the host paths are insufficient.** It could import a theme ZIP already placed on internal storage, validate it, and merge it into `.rockbox`. This is more work and should not be the first solution.

### Current release-gate sequence

1. Prove one complete V61 USB enable/export/eject/disable/return cycle.
2. In V62, mount the internal volume, merge a complete compatible `.rockbox` theme tree,
   eject safely, return to Rockbox, load the theme, and prove reboot persistence.
3. In V63, cover cancellation, unplug-before-enable, repeated connection, and
   no-stuck-volume cases.
4. If direct file copy is reliable, document it as the primary release workflow.
5. Build the desktop installer only if host file managers or platform-specific hidden
   folder handling make the direct workflow unreliable.

### Installer safety requirements

If a Y2 theme installer is required, it must:

- Accept standard Rockbox theme ZIPs/folders containing a `.rockbox` tree.
- Reject path traversal, absolute paths, symlinks, and writes outside the selected `.rockbox` root.
- Show the destination and files that will be added or replaced before writing.
- Never delete unrelated themes, music, databases, settings, or user files.
- Preserve user-added themes during Rockbox resource upgrades and normal boot.
- Warn when a package appears intended for an incompatible screen resolution or target.
- Handle hidden `.rockbox` folders on Windows, macOS, and Linux without requiring users to change global file-manager settings.
- Report partial copies and dependency problems rather than claiming success.

### USB/theme acceptance criteria

- Start on the Rockbox route, connect USB, and reach the USB-storage screen without the stock home UI appearing.
- Enable USB storage and expose the intended internal-storage volume; expose microSD as well if present.
- The computer can see and write the root `.rockbox` tree.
- Install a complete 480x360/Y1-360p-compatible theme payload, including its dependent fonts and images.
- Safely eject or turn USB storage off; the volume remounts and Rockbox returns automatically.
- The new theme appears in `Settings -> Theme Settings -> Browse Themes`, loads successfully, and survives reboot.
- Existing themes, configuration, music, and database files remain intact.
- Cancelling the USB flow, unplugging without enabling storage, and repeating the process do not leave Rockbox or the volumes stuck.
- Validate the supported workflow on Windows, macOS, and Linux, or clearly document any platform limitation.

## Feature: Bluetooth

### Goal

Allow users to open Bluetooth management from Rockbox, pair headphones or speakers, route audio over A2DP, and use media controls where supported.

### Implementation direction

- Launch `android.settings.BLUETOOTH_SETTINGS` from a Rockbox-visible entry, with the known Settings components as fallbacks.
- Preserve the stock Bluetooth apps, MTK binaries, firmware, libraries, permissions, and configuration in every package.
- Pause/background Rockbox cleanly while settings is visible, then return to Rockbox when the user exits.
- Validate adapter power, pairing, reconnect, A2DP audio routing, volume behavior, and AVRCP play/pause/previous/next.
- Do not replace Android pairing with native Rockbox Bluetooth code for the first version.

### Acceptance criteria

- Bluetooth settings opens from Rockbox without exposing the stock launcher.
- A common headset/speaker can pair, play audio, disconnect, and reconnect after reboot.
- Wired output resumes correctly after Bluetooth disconnects.
- Remote media buttons behave correctly or any unsupported actions are documented.

## Feature: Wi-Fi

### Goal

Expose and validate the Y2's Android Wi-Fi stack from the Rockbox route for future network features and maintenance tools.

### Implementation direction

- Start with `android.settings.WIFI_SETTINGS`, falling back to the known Y2 Settings activity.
- Physically prove that the adapter can turn on, scan, associate, obtain DHCP, reach the network, reconnect after reboot, and resume after sleep.
- Measure idle/battery impact and ensure Wi-Fi can be turned fully off.
- Keep Wi-Fi ADB disabled by default. If retained as a developer feature, make it explicit and temporary.

### Acceptance criteria

- Wi-Fi settings opens from Rockbox without the stock home UI taking over.
- The Y2 can join a protected network and reconnect after reboot.
- Rockbox playback remains stable during network activity and after returning from settings.
- Turning Wi-Fi off leaves no unexpected battery or boot impact.

## Feature: FM Radio

### Goal

Make the Y2's existing FM hardware/software usable from the Rockbox route.

### Implementation direction

- First launch the stock FM activity as an Android-side shortcut from Rockbox.
- Validate tune, seek, region spacing, headphone/antenna requirements, audio routing, volume, and returning to Rockbox playback.
- Keep a native Rockbox FM driver/integration as a later project; do not block the first working FM shortcut on it.

### Acceptance criteria

- FM opens from Rockbox and can tune at least one known station under suitable reception conditions.
- Audio routes predictably and Rockbox playback resumes cleanly after exit.
- Headphone/antenna and regional requirements are documented.

## Feature: Centre Press to Wake Screen

### Goal

Allow a centre click to wake the display or restore the Rockbox view. While already awake, centre remains OK/select.

### Investigation and implementation direction

- Use root diagnostics to capture `/dev/input`/key events and power-state logs while the display is off.
- If the kernel still emits centre while asleep, prefer a keylayout or Android power-policy `WAKE_DROPPED`-style solution so the wake press does not also select an item.
- If the front-wheel controller stops delivering events during sleep, root access alone cannot create the missing event; investigate the controller/kernel path before considering an always-awake workaround.
- Avoid synthetic root `input keyevent POWER` as the normal implementation.
- Debounce the wake press and suppress its matching key-up/select event.

### Acceptance criteria

- One deliberate centre press wakes the screen from the normal screen-off state.
- The wake press does not also open or activate the currently highlighted item.
- Centre still behaves as OK/select while awake.
- Battery use and accidental wakes remain acceptable.

## Optional Feature: Power Button as Hold/Lock

### Intent

- Make the Y2 power button behave like an old iPod Classic hold switch.
- Pressing power enters a Rockbox-level locked state.
- While locked, accidental button presses are ignored.
- Wheel activity may wake the screen or app view, but does not unlock by itself.
- Unlock requires a deliberate full wheel-rotation gesture.

### Implementation preference

- Implement inside Rockbox app-level input handling first.
- Do not write `/proc/tpd_keys_enable`.
- Do not rely on stock/kernel lock behavior for the first version.
- Define a full rotation from real probe data, likely as a sequence/count of wheel events rather than assuming a rotary-sensor event.

### Acceptance criteria

- Power toggles locked mode while Rockbox is active.
- Locked mode ignores normal navigation/playback actions.
- The full-wheel gesture unlocks reliably and resists accidental unlocks.
- The user cannot become stuck in an input-locked state.

## Optional Feature: Volume Long-Press Track Skip

### Intent

- Preserve volume short-press behavior.
- Add an optional long-press action:
  - Volume Up long press = next track.
  - Volume Down long press = previous track.

### Implementation preference

- Implement as an optional Rockbox setting after baseline input is stable.
- Use Android repeat/long-press event data only after a probe confirms what the Y2 emits.

### Acceptance criteria

- Short press still changes volume.
- Long press changes track without an excessive volume jump.
- The behavior is easy to disable if it conflicts with expected volume control.

## New Feature Template

Copy this section to the top of the detailed backlog when adding another idea:

```markdown
## Feature: Name

Priority: Release gate / Pre-release target / Optional polish

### Goal

What should the user be able to do?

### Current evidence

What is already known or physically proven?

### Implementation direction

- First safe approach.
- Fallback approach.

### Open questions

- What still needs investigation?

### Acceptance criteria

- What observable result means the feature is ready?
```
