# shell-tools
Little scripts to make life easier

# Screen/Window Recording Script

This is a bash script that uses `byzanz-record` to create GIF recordings of your entire screen or a specific window.

## Requirements

The script uses the following programs, which must be installed on your system:

- `byzanz-record`
- `xdotool`
- `xwininfo`
- `xdpyinfo`

## Installation

1. Save the script to a file, such as `record_screen.sh`, in your desired directory.
2. Make the script executable with the command `chmod +x record_screen.sh`.

## Usage

You can run the script with the following command:

```bash
./record_screen.sh [--window]
```

By default, the script records the entire screen. If you want to record the currently focused window instead, provide the `--window` flag.

The script creates a new GIF file in the `~/recordings` directory each time it's run. The filename is the current date and time, followed by `_recording.gif`.

Here is a brief description of what the script does:

1. If the `--window` flag is provided, the script uses `xdotool` and `xwininfo` to get the geometry (position and size) of the currently focused window.

2. If the `--window` flag is not provided, the script uses `xdpyinfo` to get the size of the screen.

3. The script then calls `byzanz-record` to create a GIF recording of the specified area of the screen. The recording starts after a delay and lasts for a specified duration.

## Script Configuration

You can configure the following parameters in the script:

- `DELAY`: The delay (in seconds) before `byzanz-record` starts recording. Default is 0.
- `DURATION`: The duration (in seconds) for which `byzanz-record` records the screen. Default is 10.
- `DIR`: The directory where the script saves the GIF files. Default is `~/recordings`.



# Jack Server Startup Script

This is a shell script to manage PulseAudio and Jack Audio Connection Kit (JACK) server using QjackCtl on a Linux system.

The script performs the following steps:

1. Checks if the script is being run as root. If it is, it prints an error message and exits.
2. Kills any running instances of PulseAudio.
3. Stops and disables the PulseAudio user service and socket.
4. Starts QjackCtl, which will in turn start a JACK server.
5. After QjackCtl is closed, the script re-enables and restarts the PulseAudio user service and socket.

## Requirements

This script relies on the following software, which must be installed on your system:

- PulseAudio
- QjackCtl

## Installation

1. Save the script to a file, for instance `jack_startup.sh`, in your desired directory.
2. Make the script executable with the command `chmod +x jack_startup.sh`.

## Usage

You can run the script with the following command:

```bash
./jack_startup.sh
```

Do not run this script as root. If the script is run as root, it will print an error message and exit.

The script will start QjackCtl, which should open a window for controlling the JACK server. You can use QjackCtl to manage your JACK server as needed. When you close QjackCtl, the script will automatically restart the PulseAudio service.

## Troubleshooting

If you encounter issues with the script, make sure:

- The script is not being run as root.
- All required software is installed.
- PulseAudio is correctly installed as a user service and socket.

## Disclaimer

This script stops the PulseAudio service while the JACK server is running. If you need to use both at the same time, this script might not be suitable for your use case. 


# Terminal Layout Management Script

This is a bash script to manage your terminal windows layout in XFCE environment on a Linux system. The script will position six terminal windows in a 3x2 grid on your screen, making it easy to multitask and monitor multiple processes at once.

## Requirements

The script requires the following programs to be installed on your system:

- `xfce4-terminal`
- `wmctrl`

## Installation

1. Save the script to a file, for example `terminals.sh`, in your desired directory.
2. Make the script executable with the command `chmod +x terminals.sh`.

## Usage

You can run the script with the following command:

```bash
./terminals.sh
```

This will open six new `xfce4-terminal` instances, each named `terminal_i_j`, where `i` and `j` are the row and column indices of the terminal in the 3x2 grid, respectively.

To stop and close all terminals opened by this script, use the `--stop` flag:

```bash
./terminals.sh --stop
```

## Script Behaviour

Here is a brief description of the script's behavior:

1. It first calculates the size of each terminal based on a grid layout.
2. It then kills any existing terminals that were previously opened by the script.
3. If the `--stop` flag is provided, the script will stop here.
4. The script opens six new terminal instances.
5. It uses `wmctrl` to move and resize the terminal windows to fit in the grid layout.

## Customization

You can configure the following parameters in the script:

- `WIDTH` and `HEIGHT`: These define the size of each terminal in pixels. By default, the script assumes a screen size of 2560x1600 pixels and divides this into a 3x2 grid. Adjust these values according to your actual screen size and desired terminal size.

## Troubleshooting

If you encounter any issues while running the script, make sure:

- You are not running the script as root.
- All the required programs (`xfce4-terminal` and `wmctrl`) are installed.
- Your screen resolution is compatible with the `WIDTH` and `HEIGHT` defined in the script.

