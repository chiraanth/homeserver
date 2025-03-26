<h1 align="center">🏠 Chiraanth's HomeServer</h1>
<p align="center">
  <img src="https://img.shields.io/badge/Built%20with-Docker-blue?logo=docker&style=flat-square" alt="Built with Docker"/>
  <img src="https://img.shields.io/github/stars/chiraanth/homeserver?style=social" alt="GitHub Stars"/>
  <img src="https://img.shields.io/badge/Status-Active-brightgreen" alt="Status"/>
</p>



Welcome to my homelab — a self-hosted powerhouse running dozens of containerized services to automate, secure, and manage everything from media to monitoring to backups. This setup is built on Docker Compose, designed to be modular, scalable, and privacy-respecting.



---

## 🚀 Features at a Glance

| Stack          | Services Included                                                                 |
| -------------- | --------------------------------------------------------------------------------- |
| **Media**      | Jellyfin, Sonarr, Radarr, Lidarr, Readarr, Bazarr, qBittorrent, Kavita, Navidrome |
| **Automation** | Watchtower, Jellyseerr, Deemix, Tidarr, Transmission, Metube                      |
| **Infra/UI**   | Nginx Proxy Manager, Portainer, FlareSolverr, Homarr, Docker OSX, Uptime Kuma     |
| **Storage**    | OpenBooks, Unmanic, Stirling PDF, Immich                                          |
| **Security**   | Pi-hole, fail2ban (manual), Docker network isolation                              |

---

## 🧰 Prerequisites

> 🚨 This repo assumes you're not scared of the terminal and know your way around Docker.

- 🐧 Linux server or Proxmox VM
- 🐳 Docker & Docker Compose (v2 recommended)
- 🧠 Basic understanding of ports, volumes, env files
- 📂 Mounted disk with enough space for media and config
- 📡 Static IP or local DNS (for Nginx Proxy Manager to shine)
- 🔒 (Optional) [Tailscale](https://tailscale.com/) or another VPN for secure remote access


---

## 📁 Directory Structure

```
homeserver/
├── docker-compose/
│   ├── media/             # Media servers and automation tools
│   ├── infrastructure/    # Network, monitoring, dashboards
├── .env.sample            # Sample environment variables
├── README.md              # This file
├── LICENSE                # MIT or whatever you choose
└── docs/                  # Guides (e.g. how to add drives)
```

---

## 🐳 Running the Stack

> 🔑 I use [Tailscale](https://tailscale.com/) to access my services remotely without exposing ports. Just install the app, log in, and everything in my private network is reachable — even from my phone.


1. **Clone the Repo:**

```bash
git clone https://github.com/chiraanth/homeserver.git
cd homeserver
```

2. **Copy and Edit Environment Variables:**

```bash
cp .env.sample .env
nano .env  # or your preferred editor
```

3. **Start Your Desired Stack:**

```bash
docker compose -f docker-compose/media/jellyfin.yml up -d
```

> 💡 You can run multiple stacks at once. Just run them in separate compose files, or combine if needed.

---

## 🧩 Service-by-Service Breakdown

> 📌 Click each service name to learn more!

### 🎞 Media Stack

Each tool is handpicked to cover a core media function:

- **[Jellyfin](https://jellyfin.org/)**: My personal streaming server. Think Plex, but open-source and tracker-free.
- **[Sonarr](https://sonarr.tv/)**: Automatically grabs TV episodes as soon as they drop.
- **[Radarr](https://radarr.video/)**: Same as Sonarr, but for movies. Pulls from indexers and automates downloads.
- **[Lidarr](https://lidarr.audio/)**: Like Radarr/Sonarr but for music albums.
- **[Readarr](https://readarr.com/)**: Books, comics, audiobooks. Set it and forget it.
- **[Bazarr](https://github.com/morpheus65535/bazarr)**: Pulls subtitles automatically and integrates with Jellyfin.
- **[qBittorrent](https://www.qbittorrent.org/)**: Lightweight torrent client. Configured with categories for automation.
- **[Kavita](https://www.kavitareader.com/)**: High-performance manga and eBook reader.
- **[Navidrome](https://www.navidrome.org/)**: Spotify-style interface for your MP3/FLAC collection.
- **[Deemix](https://gitlab.com/Bockiii/deemix-docker)**: Deezer music downloader.
- **[Tidarr](https://github.com/cstaelen/tidarr)**: Uses Lidarr-style interface for TIDAL downloads.

### 🧠 Smart Tools

- **[Immich](https://immich.app/)**: Google Photos alternative with ML-based face detection and albums.
- **[Unmanic](https://github.com/Unmanic/Unmanic)**: Real-time media file optimizer. Runs in the background to transcode or normalize media.
- **[OpenBooks](https://github.com/evanbuss/openbooks)**: Searches IRC for DRM-free books and downloads them directly.
- **[Stirling PDF](https://github.com/Frooodle/s-pdf)**: All-in-one PDF toolkit – compress, OCR, merge, split, rotate.

### ⚙️ Infrastructure / UI

- **[Tailscale](https://tailscale.com/)**: Creates a secure WireGuard mesh VPN. Lets me access all services remotely (even behind CGNAT or firewalls) without exposing any ports to the public internet.

- **[Nginx Proxy Manager](https://nginxproxymanager.com/)**: Lets me use local DNS names like `jellyfin.local` or external domains. Handles HTTPS automatically with Let's Encrypt.
- **[Portainer](https://www.portainer.io/)**: Clickable UI for managing Docker containers and stacks.
- **[FlareSolverr](https://github.com/FlareSolverr/FlareSolverr)**: Bypasses Cloudflare & bot protection for indexers.
- **[Uptime Kuma](https://github.com/louislam/uptime-kuma)**: Looks like UptimeRobot but 100x better and self-hosted.
- **[Docker OSX](https://github.com/sickcodes/Docker-OSX)**: Because why not run macOS inside a Docker container?
- **[Watchtower](https://containrrr.dev/watchtower/)**: Automatically pulls updated images and restarts containers cleanly.
- **[Homarr](https://github.com/ajnart/homarr)**: My landing page for everything. Fully customizable and beautiful.

### 🔐 Network & Security

- **[Pi-hole](https://pi-hole.net/)**: Blocks ads, trackers, and telemetry at the DNS level.
- **fail2ban (manual)**: Optional brute force protection.

---

## 🧠 Homelab Philosophy

> 🔐 "Privacy isn’t about having something to hide, it’s about having control."

I built this to own my data, reduce reliance on cloud services, and just because it’s **fun**. Everything here is:

- 🔓 Open-source
- 💡 Automated
- 📊 Monitorable
- 🔧 Easy to back up

And it’s always evolving.

---

## 🔧 Scaling & Storage

- Add new drives to your host?
- Expand an LVM pool?
- Mount and remap volumes?

➡️ [Check the guide in](./docs/add-disk-lvm-guide.md)

---

## ☁️ Future Plans

Here's what I plan to add or improve over time:

- [ ] 🔄 Automate encrypted off-site backups using [rclone](https://rclone.org/) + cron
- [ ] 🧪 Set up CI using [GitHub Actions](https://github.com/features/actions) or [Drone CI](https://www.drone.io/)
- [ ] 🧱 Add [Traefik](https://doc.traefik.io/traefik/) for advanced network segmentation and routing
- [ ] 📊 Deploy [Grafana](https://grafana.com/) + [Prometheus](https://prometheus.io/) for real-time dashboards
- [ ] 📤 Use [Tailscale](https://tailscale.com/) for secure remote access
- [ ] 🧰 Build custom [Docker](https://www.docker.com/) images for niche tools
- [ ] 🧠 Integrate [OpenAI Whisper](https://github.com/openai/whisper) for voice-to-text and local transcription
- [ ] 🛡️ Harden containers using [AppArmor](https://wiki.ubuntu.com/AppArmor) profiles and read-only mounts

---

## 🪪 License

MIT — free to use, fork, remix.

> ⭐ Star this repo if it gave you ideas. Or fork it and build something even better.

---

<p align="center">
  <strong>⭐ If you like this project, give it a star — or fork it and build your own homelab empire.</strong><br/>
  Made with ❤️ by <a href="https://github.com/chiraanth">Chiraanth</a>
</p>
