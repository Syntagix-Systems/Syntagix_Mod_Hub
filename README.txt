# Syntagix Mod Hub

**A Windows mod manager for GTA V Legacy.**

Install archives, organize your mod library, edit configuration files, and review changes made during your game sessions from one application.

Syntagix Mod Hub is developed by **Syntagix Systems**.

- **Community, support, and download announcements:** [Discord](https://discord.gg/pDB9f9p5Z5)
- **Demonstrations and project videos:** [YouTube](https://www.youtube.com/@syntagix_systems)
- **Installer:** `SyntagixModHubSetup.exe`, available from the official release or the download link shared on Discord.
- **Patreon:** Coming soon.

## Contents

1. [Requirements and installation](#1-requirements-and-installation)
2. [First-time setup](#2-first-time-setup)
3. [Pages and navigation](#3-pages-and-navigation)
4. [Installing an archive](#4-installing-an-archive)
5. [OIV packages and mixed packs](#5-oiv-packages-and-mixed-packs)
6. [Manual installation](#6-manual-installation)
7. [Managing the library](#7-managing-the-library)
8. [Dependencies and sub-mods](#8-dependencies-and-sub-mods)
9. [Editing configuration files](#9-editing-configuration-files)
10. [Launching and managing sessions](#10-launching-and-managing-sessions)
11. [Reviewing session changes](#11-reviewing-session-changes)
12. [Browsing folders and archives](#12-browsing-folders-and-archives)
13. [Settings and file analysis](#13-settings-and-file-analysis)
14. [Storage and restoration](#14-storage-and-restoration)
15. [Updating or removing the application](#15-updating-or-removing-the-application)
16. [Troubleshooting](#16-troubleshooting)
17. [Support and third-party components](#17-support-and-third-party-components)

## 1. Requirements and installation

### Requirements

- Windows x64.
- GTA V **Legacy**, with its normal game launcher available.
- Enough disk space for your managed mods, injected game copies, and temporary installation or RPF work.
- LSPDFR, RagePluginHook, and any other prerequisites required by the mods you use.

GTA V Enhanced and Windows on ARM have not been validated for this release.

**You do not need to install Python, PySide6, .NET, or 7-Zip separately to run the distributed application.** The necessary application components are bundled. This does not replace runtime requirements that other mods or game tools may have.

### Install with the Windows installer

1. Download `SyntagixModHubSetup.exe` from the official release or Discord download link.
2. Run the installer and approve the Windows administrator prompt.
3. Choose the application installation folder.
4. Optionally enable the desktop shortcut.
5. Open **Syntagix Mod Hub** from the Start menu or its shortcut.

The installer places `SyntagixModHub.exe` and its `_internal` folder together. `_internal` contains required application resources and runtimes; keep it with the executable.

### Portable distribution

If you downloaded a portable ZIP instead, extract the entire application folder and run `SyntagixModHub.exe`. Keep `_internal` beside it. Moving only the executable will leave required files behind.

The portable build still stores personal settings and library metadata in LocalAppData; it is not a fully self-contained user profile.

## 2. First-time setup

### Configure the folders

Open **Settings**, then configure:

| Setting | What to select |
| --- | --- |
| **GTA V folder** | Your GTA V Legacy installation folder, containing `GTA5.exe`. |
| **Mods folder** | A separate folder where Syntagix stores the files to inject. |
| **Modded launcher (optional)** | The executable to start for modded gameplay. For LSPDFR, configure `RagePluginHook.exe`. |

Example:

```text
D:\Games\Grand Theft Auto V\     GTA V installation
D:\Syntagix\Mods\               Managed mod files
D:\Mod Downloads\               Original downloaded archives
```

The GTA V and managed Mods folders must be on the **same drive**, and neither may be inside the other. Do not put the managed Mods folder inside the application's LocalAppData storage.

The configured **Mods folder** is different from GTA V's internal `mods` folder used for modified RPF archives. An OIV package may create a path such as this inside your managed folder:

```text
D:\Syntagix\Mods\mods\update\update.rpf
```

Its destination during injection is:

```text
D:\Games\Grand Theft Auto V\mods\update\update.rpf
```

Keep downloaded archives outside the managed Mods folder. Simply dropping a ZIP into that folder does not install or register its contents.

For the modded launcher, select an executable inside the GTA V folder. If RagePluginHook is supplied by a registered mod and has not been injected yet, you can enter the GTA-relative path `RagePluginHook.exe`; it must be available in the managed Mods folder for injection.

Click **Save changes** at the top of Settings.

### Create the vanilla baseline

1. Close GTA V.
2. Make sure the GTA V folder is clean and unmodded.
3. Open **Settings → BASELINE AND FILE ANALYSIS**.
4. Select **Create vanilla baseline** and confirm.

The baseline records the original **file and folder paths** used to identify unexpected items. It is **not a complete backup of GTA V**, does not copy the whole game, and is not a full file-integrity check.

Creating a baseline from an already modded game would treat those files as original. Resolve an existing manual installation before creating your first clean baseline.

Baseline creation is unavailable during a modding session, while files are injected, while GTA V is running, or while changed folder paths are unsaved.

## 3. Pages and navigation

| Page | Main purpose |
| --- | --- |
| **Home** | Launch LSPDFR or clean GTA V, see mod counts, and control persistent modding sessions. |
| **Library** | Search, filter, enable, disable, and configure installed mods. |
| **Install** | Select or drop an archive, or prepare a manual installation. |
| **Archives** | Browse the managed Mods folder and supported archives in read-only mode. |
| **Settings** | Configure folders, display size, categories, the baseline, and manual analysis. |

Many dialogs can be resized by dragging their edges or lower-right corner. F11 toggles fullscreen for supported application windows.

## 4. Installing an archive

1. Open **Install**.
2. Drop an archive onto the application, or click **Select an archive…**.
3. Review the detected archive structure and proposed source folder.
4. Check the installation preview and any included instructions.
5. Adjust destinations or exclude files where needed.
6. Select dependencies and any installed mods that depend on the new mod.
7. Review the final plan and confirm.
8. Resolve any file conflicts, then read the installation report.

ZIP, RAR, 7z, and supported OIV packages are accepted. Archive analysis runs locally and does not require an AI service or API key. Password-protected archives do not have a password-entry workflow.

### Choose the correct source folder

Select the folder whose **contents** belong in the GTA V root structure. Packaging folders and developer resources should not become extra destination folders.

For example:

```text
Example Mod.zip
├── FOR DEVELOPERS ONLY
└── ! GTAV MAIN DIRECTORY
    ├── plugins
    └── lspdfr
```

Choose `! GTAV MAIN DIRECTORY` as the source folder. The intended result is `plugins/...` and `lspdfr/...`, not `! GTAV MAIN DIRECTORY/plugins/...`.

Detection is a starting point. Check the author's instructions and the displayed destinations before installing.

### Review and change destinations

The wizard includes **Files to install**, **Excluded files**, **Mod instructions**, and **Folder analysis**.

To relocate content:

1. Select a file or folder in the preview.
2. Click **Change installation location…**.
3. Choose its destination inside the configured Mods folder.
4. Check the updated destination column.

For example, a folder named `VCF's Files` may need to install into `ELS/syntagix_pack`, depending on the pack's instructions. Use **Exclude selection** for unwanted content and **Reset destinations** to clear destination overrides.

Destinations outside Mods and duplicate destination paths are rejected.

### Shared-file conflicts

If another mod already uses the same path with different contents, the conflict dialog identifies the affected mods and offers the available choices:

- **Keep the existing file**.
- **Use the new file**.

Bulk choices are available where replacement is allowed. Some managed or protected shared files cannot be replaced through that dialog; resolve the owning mod or package first.

Verification compares installed files with their registered contents. It does not prove that a mod will load in-game or that all of its external requirements are installed.

## 5. OIV packages and mixed packs

### OIV installation

Supported OIV manifests are processed by the bundled tools. The installer uses working copies and publishes its output into the managed Mods folder. Original GTA V archives are read-only source material for this process.

Supported operations include file copies, supported XML edits, and top-level RPF7 additions or replacements. **Nested RPF writes and unsupported OIV instructions are rejected.** An archive containing an OIV is not automatically compatible with every operation that package requests.

The OpenIV application is not required for this installation pipeline. The bundled `OpenIV.asi` and `dinput8.dll` support components are provisioned into Mods when needed; existing components are checked rather than blindly overwritten.

### Packs containing files and multiple OIVs

Loose files and selected embedded OIV packages can be installed as **one library entry**.

When the wizard presents multiple OIVs:

1. Enable the packages you actually want.
2. Use **Move up** and **Move down** to arrange their order.
3. Follow the author's required sequence, such as base package before update.
4. Leave incompatible or unwanted variants off.
5. Review the loose files as well as the OIV selection.

Recognized optional variants start disabled. The selected OIVs are applied in their chosen order, followed by the selected loose files. Install required external prerequisites separately.

## 6. Manual installation

Use this workflow when you want to arrange a set of files yourself and add it to the library.

1. Open **Install → Manual installation…**.
2. Enter a **Mod name** and, optionally, a version.
3. Click **Open folder in Explorer**.
4. Place the files in the staging folder using their intended GTA-relative structure.
5. Return to the launcher and click **Review and continue**.
6. Review destinations and dependencies, then complete installation.

Example staging contents:

```text
plugins/
    ExamplePlugin.dll
    ExamplePlugin/
        settings.ini
ELS/
    syntagix_pack/
        example.xml
```

Do not add an extra `Grand Theft Auto V` folder around those contents.

After a successful, verified installation, the private staging job and its generated ZIP are removed. If you cancel or an error occurs, the prepared files remain. Downloaded source archives outside that private job are not deleted.

## 7. Managing the library

### Cards, selection, and filtering

Each card shows the mod's name, version, activation state, category, dependencies, and associated file or OIV operation count.

- Use the search field to find a mod.
- Click category cards to show or hide categories.
- Click a mod card to select it; click empty space to clear selection.
- Use a parent card's arrow to expand or collapse its sub-mods.

**Hiding a category only changes the view. It does not disable its mods.**

### Enable or disable a mod

Use the ON/OFF switch on the card. Wait for the operation to finish before starting another library operation.

Disabling retains the data required to enable the mod again. Shared files remain available when an active mod still needs them. Enabling may require enabling dependencies first; disabling a dependency can prompt you to disable its dependent mods as well.

### Mod configuration

Click the **gear icon** beside the switch to open **Mod configuration**.

You can change the name, version, category, dependencies, and parent relationship. The green **Save** button becomes available when those properties change.

The dialog also provides:

| Action | Purpose |
| --- | --- |
| **Configure files** | Open registered XML and INI files in the editor. |
| **Verify installation** | Check registered files against their expected contents. |
| **Update** | Replace an eligible standard mod with a new archive version. |
| **Uninstall** | Remove the mod and apply the appropriate shared-file restoration. |

### Update a mod

The current **Update** action requires the game session to be finished and injected files cleaned up. The standard mod must be enabled.

Choose the new archive and review the proposed changes. Old exclusive files missing from the new version can be removed; incompatible shared files can block the update.

OIV updates use the **Install** workflow. A standard mod with custom destination mappings must be uninstalled and reinstalled through the wizard to review the new archive's destinations. Keep any configuration changes you want before replacing or uninstalling a mod.

### Uninstall a mod

Open its gear dialog, select **Uninstall**, and confirm. Files exclusively belonging to that mod are removed; shared or displaced versions are handled according to their registered owners.

A parent mod with attached sub-mods must have those relationships resolved before removal. Active dependencies may also need to be resolved first. During a tracked session, game-folder removals are deferred until cleanup.

## 8. Dependencies and sub-mods

These relationships serve different purposes:

| Relationship | Use it when… |
| --- | --- |
| **Dependency** | A mod requires another installed mod to function. |
| **Sub-mod** | An extension or customization belongs under a parent mod in the library. |

### Set dependencies

In **Mod configuration**, switch **This mod has dependencies** on, select the required mods, and save. During archive installation, the wizard also asks whether installed mods depend on the new one.

Dependency selection lists principal mods rather than individual sub-mods. It records relationships; it does not download missing prerequisites. Dependency cycles are rejected.

### Assign a sub-mod

Switch **This mod is a sub-mod** on, choose its **Parent mod**, and save.

For example, a UI replacement can appear indented under the plugin it customizes. The parent relationship also participates in dependency handling. Sub-mods use the parent's displayed category in the library.

## 9. Editing configuration files

1. Open a mod's gear dialog.
2. Click **Configure files**.
3. Choose a registered XML or INI file from the left-hand list.
4. Edit its contents; use search and replacement if needed.
5. Click **Preview changes** to inspect the differences.
6. Click **Save all files**, or press **Ctrl+S**, and confirm.

The editor works with registered, accessible loose XML and INI files. It is not an editor for files inside RPF archives.

Saved changes update the managed Mods files. During a tracked session, the launcher also attempts to publish them to GTA V immediately. If Windows prevents a copy, Mods retains the saved version and the deferred game copy is reported.

For plugins that support it, run `ReloadAllPlugins` yourself in the RagePluginHook console to reload settings without restarting GTA V. The launcher does not issue that command, unload plugins, or guarantee that every change can be reloaded. Vehicles, DLC, and some other resources require a game restart.

There is no permanent automatic history of every configuration edit.

## 10. Launching and managing sessions

### Launch LSPDFR

1. Configure the folders, RagePluginHook launcher path, and vanilla baseline.
2. Install and enable the required mods and prerequisites.
3. On **Home**, click **Launch LSPDFR** and confirm.
4. Keep Syntagix Mod Hub open while playing.

The launcher prepares the enabled content and waits for its injection operation to finish **before starting the configured game launcher**. If preparation fails, the game is not launched through that operation.

### Launch clean GTA V

Click **Launch clean GTA V**. The launcher performs the required review and cleanup, then checks for unknown items or unrestored backups before starting the normal GTA V launcher.

A clean launch is based on Syntagix's baseline and tracked state. It is not a complete verification of every original game file.

### Persistent modding session

The **Modding session** control at the bottom of Home shows **Active** or **Inactive**:

- **Inactive:** after a tracked game session ends and its changes are reviewed, injected files are cleaned up.
- **Active:** the modded working state can remain between game launches. End the persistent session when you want to clean up the game folder.

Keep the launcher running so it can monitor the game and present the end-of-session review.

### Changes while playing

These behaviors apply to a **tracked Syntagix session**:

| Operation | Managed Mods folder | GTA V folder |
| --- | --- | --- |
| Install or enable a mod | Updated immediately. | Available files are copied immediately; locked or unavailable copies are deferred. |
| Save a configuration edit | Updated immediately. | An immediate copy is attempted; deferred copies are reported. |
| Disable or uninstall a mod | Updated immediately, with shared-file handling. | Tracked removals wait for cleanup after the game closes. |
| Use the existing mod's **Update** action | Requires ending the session first. | Not a live-session update workflow. |

Copying a file does not automatically refresh a resource already loaded in memory. Syntagix does not bypass Windows file locks.

## 11. Reviewing session changes

When a tracked game session ends, review the changes before cleanup. Persistent modding mode can keep the working state injected after that review.

The report separates changes into three groups:

| Group | Apply | Skip |
| --- | --- | --- |
| **Modified files** | Save the session version back into Mods. | Preserve the Mods version and discard the session modification. |
| **New GTA V files** | Copy the new file into Mods. | Do not keep it; it is removed from GTA V during the review workflow. |
| **Files deleted from GTA V** | Remove the corresponding managed file from Mods. | Keep the file in Mods for a future session. |

Use the individual toggles, or **Apply all** and **Skip all** within a group, then click **Apply choices**. Canceling postpones the review and cleanup.

**Example:** if three files were deleted in-game but one deletion was accidental, apply the two intended deletions and switch the accidental one to **Skip**. The skipped file remains in Mods.

New files can be assigned to an eligible active standard mod or kept unassigned in Mods. They do not automatically create a generic mod entry in the library.

Library actions already performed during the session, such as uninstalling a mod, are tracked separately so session synchronization does not undo those decisions.

A report records the applied and skipped operations. Cleanup removes tracked injected files, restores originals that were set aside, and removes empty managed session directories. It does not delete nonempty directories indiscriminately.

## 12. Browsing folders and archives

Open **Archives** to browse the managed Mods folder.

- Double-click a folder to enter it.
- Double-click a supported archive to browse its contents.
- Double-click a supported text file to preview it.
- Double-click the **`..`** row to go up.
- Use the mouse side-back button to return to the previous location.
- Click empty space to clear the selection.

This explorer is **read-only**. It does not create folders, import files, edit archive contents, or render 3D models and textures. Large previews and unsupported binary files are limited or refused. RPF access depends on the bundled reader and supported GTA V archive formats.

Use **Configure files** for loose XML/INI editing and **Install** to add managed content.

## 13. Settings and file analysis

### Display size

Choose **Small**, **Normal**, or **Large** under **DISPLAY SIZE**, then save. A check mark identifies the current choice in the list.

### Categories

The default categories are **Plugins**, **Graphics**, **Audio**, and **Others**.

- Click **Add category** to create one.
- Click a category card to rename or delete it.
- Use **Move left** or **Move right** in its dialog to change the order.
- When deleting, choose the destination category for its mods and confirm twice.
- Click **Save changes** at the top of Settings to commit the changes.

The library uses the saved category order. Deleting a category reassigns its mods; it does not uninstall them.

The top Save button is green when changes are pending and muted when settings are saved. Leaving Settings with unsaved changes offers to discard them or return.

### Baseline viewer and manual analysis

- **View vanilla baseline** opens the saved file and folder inventory without changing GTA V.
- **Analyze files…** opens a manual review of unknown items relative to that inventory and tracked state.

The unknown-file review provides **Move to Mods**, **Accept as vanilla**, **Quarantine**, and **Refresh**, plus **Clean up folder**.

Choose **Accept as vanilla** only for an item you intend to treat as part of the original installation. Quarantine moves an item to a recoverable trash location. Manual classification requires the game to be closed and injected files removed; if a tracked cleanup is blocked by unknown items, finish the session review first and follow the reported recovery instructions rather than deleting tracking data.

### Danger zone: delete the library

At the bottom of Settings, **Delete library…** is a destructive reset. It requires saved settings, a closed game, no injected session or active library operation, and typing **DELETE**.

It deletes:

- **All contents of the configured managed Mods folder**, including unrelated files stored there.
- Registered mods and related stored versions or backups.
- Managed OIV package caches and receipts.
- Related installation/session reports and temporary library data targeted by the reset.

It preserves configured folder paths, category preferences, the vanilla baseline, original GTA V files, and downloaded archives **outside** Mods.

This operation cannot be undone. Use it only when intentionally starting a new library.

## 14. Storage and restoration

### Storage locations

| Location | Contents |
| --- | --- |
| Application installation folder | The executable and `_internal` resources. |
| Configured managed Mods folder | Current files used for injection. |
| GTA V folder | Original game files and the tracked session's working copies. |
| `%LOCALAPPDATA%\Syntagix_Launcher` | Settings, registry metadata, stored versions, receipts, reports, and working data. |
| Your chosen download folder | Original archives you downloaded yourself. |

The LocalAppData name remains `Syntagix_Launcher` for continuity with existing installations.

### Standard mods

Current active contents live in Mods. The launcher retains displaced or disabled versions when needed for restoration, rather than making a permanent copy of every installed file. Identical stored versions can be shared.

When replacing an existing unmanaged loose file, the original version is retained so it can be restored when appropriate. Unused stored versions are removed once no registered mod needs them.

### OIV packages

OIV layers use original GTA V source files and retained package data to rebuild supported outputs. A permanent full initial backup is not kept for every unowned OIV output.

Active and disabled packages retain data needed for replay or reactivation. Uninstalling removes unused private package data and receipts. Your separately downloaded source archives are kept.

Some restoration scenarios involving an existing custom RPF provider still require a full archive copy. Storage is not a binary-delta system. An unknown custom RPF can be refused when its origin cannot be established safely.

### Game restoration files

If injection replaces an original GTA V file, a `.vanillabak` file can be required to restore it during cleanup. Do not remove these files or the active session's tracking data before the session has been resolved.

Reports retain decisions and file metadata; they are not complete copies of every historical configuration. The storage policy reduces duplication but is not a substitute for your own backup of important custom settings.

## 15. Updating or removing the application

### Update Syntagix Mod Hub

1. Close GTA V.
2. Complete the session review and cleanup; end persistent modding mode if active.
3. Close Syntagix Mod Hub.
4. Run the new installer and use the existing application location.

For a portable build, extract the complete new application folder and keep its executable and matching `_internal` together. Do not mix resources from different builds.

Settings and library metadata live outside the application folder and are preserved by the installer. Keep both the managed Mods folder and its matching LocalAppData metadata when preserving a library.

### Uninstall Syntagix Mod Hub

Finish the game session and cleanup first, then use Windows **Installed apps** to uninstall the application.

The Windows uninstaller deliberately preserves personal library data, the managed Mods folder, and GTA V files. Removing the application is different from choosing **Delete library…** inside Settings.

## 16. Troubleshooting

| Issue | What to check |
| --- | --- |
| The application does not start. | Keep the matching `_internal` folder with the executable. Check `%LOCALAPPDATA%\Syntagix_Launcher\startup_error.log` if present. |
| A folder is rejected. | Use GTA V Legacy's root, keep the managed Mods folder separate, and use the same drive. Save changed paths before creating a baseline. |
| Launch is blocked by unknown files. | Open **Settings → Analyze files…** and review the reported items. Do not create a new baseline just to hide mod files. |
| The modded launcher is outside GTA V. | Configure the GTA-side `RagePluginHook.exe` path or its GTA-relative name, not an executable in a separate download folder. |
| A mod is installed but does not load. | Check the selected source folder, final destinations, game/mod versions, external prerequisites, and the author's loading instructions. File verification alone does not test in-game loading. |
| A change is not visible in-game. | Confirm it was saved, check deferred-copy messages, and reload the plugin if supported. Some resources require restarting the game. |
| A file cannot be edited. | It must be a registered, accessible loose XML or INI file. Resolve external modifications, links, or locking errors reported by the editor. |
| An OIV is refused. | Read the preflight error. Nested RPF writes or unsupported manifest operations need another installation method. |
| An activation switch is unavailable. | Wait for the current operation, resolve dependencies, and read any ownership or legacy OIV restoration error. Do not delete receipts to force an operation. |
| Drag and drop is unavailable. | Use **Select an archive…** to select the same supported file. |
| The baseline button is disabled. | Close the game, complete cleanup, end modding mode, and save folder settings. |
| Cleanup is incomplete. | Keep tracking and restoration files, close GTA V fully, and follow the report. Do not remove `.vanillabak` files to dismiss the error. |
| A mod's Update action is blocked. | End the session, clean up injection, and enable the mod. OIVs and custom-destination reinstalls use the Install workflow instead. |

Installation and verification reports are stored under `installation_reports`; session decisions are stored under `session_reports` in the application data folder. The main application log is `syntagix_v2.log` in that same folder; its filename is retained for compatibility.

## 17. Support and third-party components

For support, include the exact error, steps to reproduce it, archive or mod version, whether a session was active, and the relevant report. Explain whether **Verify installation** passed and what happened in-game.

- **Discord:** [Join the Syntagix Systems community](https://discord.gg/pDB9f9p5Z5)
- **YouTube:** [Syntagix Systems](https://www.youtube.com/@syntagix_systems)
- **Downloads:** Check the official release or the download link announced on Discord.
- **Patreon:** Coming soon.

The application bundles third-party components and their applicable notices, including archive tools, Python/Qt components, a private .NET runtime, and GTA archive support components. Retain the license and notice files distributed with the application. Individual mods remain the work of their respective authors.
