# DroidSync

A CLI tool that uses Android Debug Bridge (ADB) to **back up and restore app data** from one Android device to another — no root required.

![usage](https://user-images.githubusercontent.com/111997815/231152359-449df2f1-b776-40e6-815e-db4520af3008.png)

> Developer: `Dev. Gautam Kumar`

## What it does

DroidSync runs `adb backup` for a target package (data only, **no APK**), then automatically restores that backup to the attached device, letting you move app data between phones.

## Requirements

- Android Debug Bridge (`adb`) installed and on your `PATH`
- A phone connected over USB with **USB debugging** enabled (`Developer options → USB debugging`)
- Bash (Linux/macOS/WSL)

## Installation

```bash
git clone https://github.com/devsdenepal/DroidSync.git
cd DroidSync
chmod +x droidsync
# optional: add the folder to your PATH
```

## Usage

```bash
./droidsync <package.name> <file_name>.ab
```

Example:

```bash
./droidsync com.whatsapp whatsapp-data.ab
```

The script prints your device info (manufacturer, model, Android version), creates `<file_name>.ab`, and after ~15 seconds prompts the restore.

> On restore, ADB shows a confirmation dialog on the phone — tap **Restore my data**.

## How it works

```
adb backup -f <file>.ab -noapk <package>   # backup data, skip APK
adb restore <file>.ab                       # restore onto the device
```

## Troubleshooting

| Issue                                                       | Fix                                         |
| ----------------------------------------------------------- | ------------------------------------------- |
| `Device is not attached`                                    | Check cable, enable USB debugging, tap "Allow" on phone |
| `adb: no devices/emulators found`                            | Run `adb devices`; if "unauthorized", accept the prompt on your device |
| `command not found: adb`                                    | Install platform-tools and add to `PATH`    |
| Restore does nothing                                        | Accept the "Restore my data" dialog on the device (it appears after a delay) |

## License

[GPL-3.0](LICENSE)