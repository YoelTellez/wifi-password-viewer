# 📶 Wifi Password Viewer

A small **Python** project that lets you view the passwords of Wi-Fi networks saved on your system and generate a **QR code** to share the connection easily.

## ✨ Features

- Lists the Wi-Fi profiles saved on the machine.
- Lets you pick a network by its index.
- Shows the password of the selected network.
- Prints a **ASCII QR code** using the standard `WIFI:T:WPA2;S:<ssid>;P:<password>;H:false;;` format, ready to scan with a phone.

## 🖥️ Compatibility

| Operating system | Status | Tool used |
| --- | --- | --- |
| Windows | ✅ | `netsh wlan show profiles` |
| Linux | ✅ | `nmcli` (NetworkManager) |
| macOS | ❌ | Not supported yet |

## 📋 Requirements

- **Python 3.10 or newer** (the code uses `match`/`case`).
- The [`qrcode`](https://pypi.org/project/qrcode/) package.
- On **Linux**: `nmcli` (NetworkManager) installed and permission to read saved connections.

## ⚙️ Installation

```bash
git clone https://github.com/<your-username>/wifi-password-viewer.git
cd wifi-password-viewer

# Install the dependency
pip install qrcode
```

> On Linux, if you don't have `nmcli`, install it with your distribution's package manager, for example:
> `sudo pacman -S networkmanager` (Arch) or `sudo apt install network-manager` (Debian/Ubuntu).

## 🚀 Usage

Run the script with Python:

```bash
python Wifi_Pass_Viewer
```

You should see something like:

```text
Available Wi-Fi Profiles:
1 -> MyWifiNetwork
2 -> AnotherNetwork
Enter the index of the profile to view the password: 1
Password for MyWifiNetwork: mypassword123
```

After that, the QR code is printed in the terminal. Scan it with your phone's camera to connect to the network automatically.

## 🧠 How it works

- **Windows:** gets the profiles with `netsh wlan show profiles`, queries the clear-text key with `netsh wlan show profile name="<network>" key=clear`, and extracts the `Key Content` value.
- **Linux:** lists Wi-Fi connections with `nmcli -f NAME,TYPE connection show | grep wifi` and reads the PSK with `nmcli -s -g 802-11-wireless-security.psk connection show '<network>'`.
- **QR code:** builds a `WIFI:` URI containing the SSID and password, then renders it in the terminal with `qr.print_ascii()`.

## 📝 Notes and pending improvements

- macOS is not implemented yet.
- The password is printed in full in the terminal, so be careful when sharing your screen.
- Possible improvements: save the QR code as a `.png` image, a repeatable menu, and error handling for invalid input.

## ⚠️ Disclaimer

This project was created for **educational purposes** . Only use it on devices and networks you are authorized to access.

## 📄 License

No license has been specified yet.
