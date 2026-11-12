<div align="center">

<img src="snap/gui/sniffnet.png" alt="Sniffnet logo" width="128" />

# Sniffnet

**Explore network traffic, connections and saved packet captures.**

[![sniffnet](https://snapcraft.io/sniffnet/badge.svg)](https://snapcraft.io/sniffnet)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64, arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Sniffnet](https://github.com/GyulyVGC/sniffnet), a native desktop network analyzer with traffic charts, filters, reports and notifications.

</div>

---

## Getting Started

<a href="https://snapcraft.io/sniffnet"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install sniffnet
sniffnet
```

Choose a saved packet capture from your home directory to analyze it.

### Live capture

Live capture needs raw network access, which only root has. Connect the interfaces once, then run Sniffnet with `sudo`:

```bash
sudo snap connect sniffnet:network-control
sudo snap connect sniffnet:network-observe
```

On a graphical session, allow root to open a window for the duration of the run:

```bash
xhost +SI:localuser:root
sudo sniffnet
xhost -SI:localuser:root
```

`xhost +SI:localuser:root` lets local root processes use your display until you revoke it or log out. Run the last command when you are done.

## Configure

Use the application's settings. Run `sniffnet --config-path` to locate its configuration. Normal-user settings stay inside `~/snap/sniffnet/current`; there are no `snap set` options.

For captures, reports or custom resources on removable storage:

```bash
sudo snap connect sniffnet:removable-media
```

## Limitations

- Live capture works only as root. Settings for root runs live in `/root/snap/sniffnet`, separate from your user settings. Notification sounds may be silent under `sudo`.
- The bundled libpcap omits Bluetooth, D-Bus, RDMA and netfilter (NFLOG/NFQUEUE) capture, which strict confinement would block.
-Top-level hidden home directories and files outside permitted locations remain confined.
- If GPU rendering fails, try `ICED_BACKEND=tiny-skia sniffnet`.
- Updates come through `snap refresh sniffnet`.

## Build

```bash
git clone https://github.com/sidalit/sniffnet-snap.git
cd sniffnet-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/sniffnet-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/GyulyVGC/sniffnet/issues).

## License

Snap packaging: [MIT](LICENSE).
