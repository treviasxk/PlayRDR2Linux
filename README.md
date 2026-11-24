# Play RDR 2 Linux

A lightweight executable wrapper designed to improve the experience of running Rockstar Games titles through the Epic Games Launcher on Linux.

PlayRDR2Linux provides a compatibility layer that intercepts the game's launch process, initializes the Rockstar Games Launcher, and starts the original game with the required Epic Games integration parameters.

![Preview](Screenshots/banner.png)

## Supported Games

- **Red Dead Redemption 2**.
- **[Grand Theft Auto V](https://github.com/treviasxk/PlayGTAVLinux)** — Legacy and Enhanced editions.

## Features

- Supports Epic Games Launcher Flatpak and Heroic Games Launcher.
- Initializes the Rockstar Games Launcher before starting RDR2.
- Passes the original Epic Games launch arguments to the game.
- Optional startup console and diagnostic logs.

## Installation

### 1. Download

Go to the [Releases page](https://github.com/treviasxk/PlayRDR2Linux/releases) and download the `PlayRDR2Linux.zip` archive.

### 2. Install the wrapper

Extract the ZIP archive into the root directory of your RDR2 installation.

The files should look like this:

```text
Red Dead Redemption 2/
├── PlayRDR2Linux.exe
├── EpicGamesLauncher.exe
├── PlayRDR2.exe
└── ...
```

Make sure both wrapper executables are in the same directory as the original game files.

### 3. Configure your launcher

Choose the launcher you use and follow the corresponding instructions.

#### Epic Games Launcher (Flatpak)

The Epic Games Launcher Flatpak stores game installation information in:

```text
~/.var/app/com.epicgames.launcher/data/com.epicgames.eglv2/installations.jsonl
```

1. Completely close the Epic Games Launcher.
2. Open `installations.jsonl` with a text editor.
3. Find the RDR2 installation entry. Check its `dir` field to identify the correct game directory.
4. In the corresponding installation entry, change all `launchExecutable` properties to:

```json
"launchExecutable": "PlayRDR2Linux.exe"
```

5. Save the file and reopen the Epic Games Launcher.

**Important:**
* You need to update GE-Proton to version 11, this version is required to launch the Rockstar Launcher correctly. Epic Games uses GE-Proton version 10-34, located at `~/.var/app/com.epicgames.launcher/data/com.epicgames.eglv2/compat/runtime/GE-Proton10-34`. Download the latest version of GE-Proton from the [Releases](https://github.com/GloriousEggroll/proton-ge-custom/releases) page and replace all the files inside the `GE-Proton-10-34` folder with the files from `GE-Proton-11-XX`.

* `installations.jsonl` uses JSON Lines format, with one JSON object per line. Preserve the existing entries and fields. If multiple records exist for the same installation, make sure the most recent record also has `PlayRDR2Linux.exe` as its launch executable.

* If you specify an executable that does not exist within the game folder, the Epic Games Launcher will consider the game to have been removed, and it will not appear in your library until you provide a valid, existing file for that parameter.

#### Heroic Games Launcher

1. Open Heroic Games Launcher.
2. Select Red Dead Redemption 2.
3. Open **Settings → Advanced**.
4. Find **Select Alternative EXE**.
5. Select `PlayRDR2Linux.exe` inside your RDR2 installation directory.

### 4. Launch the game

Start RDR2 normally through your configured launcher.

The wrapper will automatically:

## Command Line

### Show logs

By default, the wrapper runs without displaying a console window.

To enable the console and display diagnostic information, add:

```bash
-logs
```

## Build from Source

If you want to compile the project yourself instead of downloading a pre-built release, follow these steps.

### 1. Install dependencies

On Arch Linux:

```bash
sudo pacman -S git cmake mingw-w64-gcc
```

### 2. Clone the repository

```bash
git clone https://github.com/treviasxk/PlayRDR2Linux.git
cd PlayRDR2Linux
```

### 3. Build

Configure the Windows cross-compilation build using the project's CMake toolchain file:

```bash
cmake -S PlayRDR2Linux -B PlayRDR2Linux/build -DCMAKE_TOOLCHAIN_FILE=windows.cmake
cmake -S EpicGamesLauncher -B EpicGamesLauncher/build -DCMAKE_TOOLCHAIN_FILE=windows.cmake
```

Compile the project:

```bash
cmake --build PlayRDR2Linux/build/ --config Release
cmake --build EpicGamesLauncher/build/ --config Release

# The **PlayRDR2Linux.exe** file will be located at `PlayRDR2Linux/build/PlayRDR2Linux.exe`
# The **EpicGamesLauncher.exe** file will be located at `EpicGamesLauncher/build/EpicGamesLauncher.exe`
```

## Requirements

- GE-Proton version 11-XX
- Epic Games Launcher (Flatpak) or Heroic Games Launcher
- A working RDR2 installation

## Contributing

Contributions, bug reports, and suggestions are welcome.

Feel free to open an issue or submit a pull request.

## Donate

If you enjoy this project or find it useful, consider supporting its development.

All donation methods are available on the official donation page:

**[Support this project](https://treviasxk.devs.surf/donate)**

Every contribution is appreciated and helps support continued development.
