# 🧊 Iceberg OS

A hobby operating system with a graphical desktop, its own web browser, a built-in app store, an update system, and a from-scratch TLS 1.3 stack. Built for fun, one feature at a time.

> **Status:** early beta (currently 0.11.x). Expect rough edges. Tested in VirtualBox.

---

## What's in it so far

### Desktop and apps
- Graphical desktop with windows and desktop icons
- **Notepad** with a proper *Save As* dialog: choose the file name, `.txt` or `.html`, and where to save (saves to the local disk)
- **Copy and paste** commands
- Startup sound, plus a globe icon for the browser

### Web browser
- Built-in browser that loads real websites
- Direct **HTTPS**, no proxy needed
- Typed bare names (like `example.com`) try `https://` first, then fall back to `http://`
- Missing proxy is remembered for 20 seconds so pages don't stall

### Networking and security
- Own TCP engine (`tcp.c`) with ARP replies and 1460-byte segments
- **TLS 1.3 client** written from scratch, including the crypto
- **Certificate checking** against a built-in trust store of 33 root certificates
- Timing line in the Updates log and the `net` command, for spotting slow connections

### Install to disk
- Setup option that writes the boot files to the local drive
- Boots without the ISO afterwards, and saves your files locally

### 🛒 Ice Store
- A web page that lists apps made only for Iceberg OS
- Apps use the `.app` extension and download straight into `Home/Downloads`
- Open it from the **Ice Store** desktop shortcut, or visit: https://dy2097441-coder.github.io/ice-store/
- Opening a `.app` runs it in its own window

### 🔄 Update system
- **Updates** icon on the desktop with a check-for-updates log
- Updates come as `.upt` files, followed by a restart prompt
- Shows "your PC is up to date" when there's nothing new
- Update site: https://dy2097441-coder.github.io/ice-updates/

| Update | Version | What it added |
|---|---|---|
| #1 | 0.11.1 | Cursor fix |
| #2 | 0.11.2 | New TCP engine, ARP replies |
| #3 | 0.11.3 | Crypto, TLS 1.3 client, certificate checking, trust store, direct HTTPS |
| #4 | 0.11.4 | Faster secure fetch, missing-proxy memory, bare names try HTTPS first, timing line |

---

## Running Iceberg

1. Download the ISO from the Releases page.
2. Create a new VM in **VirtualBox** and boot from the ISO.
3. For sound, set the audio controller to **ICH AC97**.
4. Optional: use the setup option to install Iceberg to the virtual disk so it boots without the ISO.

If a tool on your host needs the helper proxy (for example for update downloads), start the proxy **before** opening VirtualBox, and bind it with `--bind 0.0.0.0` so the VM can reach it. Large `.upt` files need `--max-upt`.

---

## Roadmap

- Extend the `.app` script format with clickable buttons, variables and simple maths
- A **Calculator** as an Ice Store `.app` download (not built into the OS)
- More Ice Store apps
- More updates through the update site

---

## Credits

Startup sound: *Glitch019 / Computer Startup* by Zeraora ([freesound.org/s/572773](https://freesound.org/s/572773)), CC0.

---

## Community

Join the public Discord server: https://discord.gg/M9C3223VEU

## Contributing

Ideas, bug reports and `.app` submissions are welcome. Open an issue or share them on the Discord.

## License

Add your license here (MIT is a common choice for hobby projects).
