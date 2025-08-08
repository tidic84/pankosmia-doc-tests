---
layout: default
title: Electron tips
permalink: /electron-tips/
parent: Electronite
---
# Electron tips

## Windows
{:toc}

### Goal

It is a little guide that explains how I did to develop quickly on the Electron app while using a local dev server, then produce a Windows installer locally or via CI.

### Prerequisites

* Complete the project README “Setup” for Pithekos first (dependencies, cloning, initial scripts).
* Windows 10/11
* Git, Node.js, npm, rust
* Inno Setup 6 at `C:\Program Files (x86)\Inno Setup 6\ISCC.exe`
* PowerShell allowed to run scripts

### Quick dev flow with the standalone install

1. Install the standalone Pithekos app standalone and locate its installation folder.
2. You can Edit the Electron bootstrap file which is what i did:
   * File: `electron/electronStartup.js` (inside the installed app folder)
3. Start the dev server from this repo using the provided script:
   * Script: `windows/scripts/run.bat` 

4\) Launch the Electron app from the installed folder (or via the shortcut):

* `appLauncherElectron.bat` (it's better than the shortcut bcs it shows the electron output)

### Build a Windows installer

First you have to copy your modified `electronStartup.js` (also preload.js if modified) back into the pithekos repo so they are versioned:

* Copy to: `buildResources/electron/electronStartup.js`

Then you have two options:

* Option 1 — GitHub Actions (recommended for releases)
  * Manually dispatch `buildMaster.yml` and wait for the Windows job (\~30 min).
* Option 2 — Local build (faster for iteration)
  * From the repo root, in a bash terminal:
    * You can reexcute the scripts (app\_setup, clone, etc.. (but not really necessary i guess))
    * then launch theses two script to build the electron installer
    `windows\install\bundle_zip.ps1`

    `windows\install\makeAllInstallsElectronite.ps1`

* Outputs:
  * ZIP: `releases/windows/<run.batp>-windows-<version>.zip`
  * Electron installer (x64): `releases/windows/intel64/*.exe`

Advantages of local builds:

* You can build against your current workspace state, including clients/assets checked out on feature branches.
