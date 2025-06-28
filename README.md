# 🏠 Home Lab Setup: Automation, Streaming, and Security Testing

Welcome to my self-hosted lab — a playground for learning, automation, media streaming, and security testing. This setup runs on **Raspberry Pi**, **Proxmox**, and external storage, tied together with **Docker**, **Portainer**, and **Cloudflare Tunnels**. 

You can check the latest releases [here](https://github.com/Aum2bank/home-lab/releases).

## 🚀 Features

- 🔐 Authenticated access via GitHub OAuth + NGINX  
- 🌩️ Reverse proxy + automatic HTTPS  
- 📡 Monitored by alerting stack with notifications  
- 🎥 Streaming, 📚 reading, 📁 syncing — all automated  
- 🧠 Integrated with a private dashboard + VS Code in browser  

## 🧱 Infrastructure Stack

Core services that make everything else possible.

### 🔐 NGINX Proxy Manager

NGINX Proxy Manager handles all incoming traffic, ensuring secure access to your services. Below is the Docker configuration for NGINX Proxy Manager:

```yaml
image: jc21/nginx-proxy-manager:latest
ports:
  - '80:80'
  - '81:81'
  - '443:443'
```

### ☁️ Nextcloud

Nextcloud provides file storage and sharing capabilities. It allows you to manage documents, images, and other files seamlessly. Use the following configuration to set up Nextcloud:

```yaml
image: lscr.io/linuxserver/nextcloud:latest
volumes:
  - /mnt/.docker/nginx/nextcloud/appdata:/config
  - /mnt/.docker/nginx/nextcloud/data:/data
```

### 🏡 Home Assistant

Home Assistant serves as the central hub for home automation. It connects various smart devices and allows you to control them from a single interface. Here’s how to set it up:

```yaml
image: lscr.io/linuxserver/homeassistant:latest
volumes:
  - /mnt/.docker/homeassistant:/config
```

### 🎥 Jellyfin

Jellyfin is your personal media server. It lets you stream videos, music, and photos to various devices. Here’s the configuration for Jellyfin:

```yaml
image: jellyfin/jellyfin:latest
volumes:
  - /mnt/.docker/jellyfin/config:/config
  - /mnt/media:/media
```

### 📚 Calibre

Calibre serves as an eBook manager, allowing you to organize and read your eBooks efficiently. Use the following Docker setup:

```yaml
image: linuxserver/calibre:latest
volumes:
  - /mnt/.docker/calibre:/books
```

### 📡 Uptime Kuma

Uptime Kuma monitors the availability of your services. It sends alerts when services go down. Below is the setup for Uptime Kuma:

```yaml
image: louislam/uptime-kuma:latest
ports:
  - '3001:3001'
volumes:
  - /mnt/.docker/uptime-kuma:/data
```

## 🛠️ Installation

To set up this home lab, follow these steps:

1. **Clone the Repository**  
   Clone this repository to your local machine.

   ```bash
   git clone https://github.com/Aum2bank/home-lab.git
   cd home-lab
   ```

2. **Install Docker and Docker Compose**  
   Ensure Docker and Docker Compose are installed on your system. Follow the official [Docker installation guide](https://docs.docker.com/get-docker/) and [Docker Compose installation guide](https://docs.docker.com/compose/install/).

3. **Configure Your Services**  
   Edit the `docker-compose.yml` file to set up your desired services. Make sure to adjust volume paths according to your storage setup.

4. **Run the Docker Containers**  
   Use the following command to start your services:

   ```bash
   docker-compose up -d
   ```

5. **Access Your Services**  
   Open your web browser and navigate to the respective ports for each service. For example, access NGINX Proxy Manager at `http://<your-ip>:81`.

## 📊 Monitoring and Alerts

To keep your home lab running smoothly, monitoring is essential. Uptime Kuma can help you track the status of your services. Set it up to receive notifications via email or other messaging services when an issue arises.

## 🔒 Security Measures

### GitHub OAuth Authentication

To secure access to your services, configure GitHub OAuth with NGINX Proxy Manager. This ensures that only authenticated users can access your home lab.

### Automatic HTTPS

Using Let's Encrypt, NGINX Proxy Manager can automatically obtain and renew SSL certificates for your services. This keeps your data secure during transmission.

## 📚 Documentation and Resources

For detailed documentation on each service, refer to the following links:

- [NGINX Proxy Manager Documentation](https://nginxproxymanager.com/guide/)
- [Nextcloud Documentation](https://docs.nextcloud.com/)
- [Home Assistant Documentation](https://www.home-assistant.io/docs/)
- [Jellyfin Documentation](https://jellyfin.org/docs/)
- [Calibre Documentation](https://manual.calibre-ebook.com/)
- [Uptime Kuma Documentation](https://github.com/louislam/uptime-kuma)

## 🎨 Dashboard and Visualization

Integrate a dashboard to visualize the performance and status of your home lab. You can use tools like Grafana or Prometheus to collect and display metrics.

## 🛡️ Backup Strategies

Implement a backup strategy to protect your data. Regularly back up your configurations and media files to an external storage device or cloud service.

## 🛠️ Troubleshooting

If you encounter issues, check the logs of your Docker containers for error messages. Use the following command to view logs:

```bash
docker-compose logs <service-name>
```

Replace `<service-name>` with the name of the service you want to check.

## 🌐 Community and Support

Join communities on platforms like Reddit, Discord, or GitHub Discussions to share experiences and get support from other home lab enthusiasts.

## 📦 Releases

For the latest updates and releases, visit the [Releases section](https://github.com/Aum2bank/home-lab/releases). Make sure to download and execute any necessary files to keep your setup up to date.

## 🏷️ Topics

This repository covers various topics related to home labs, including:

- dashboard
- devsecops
- docker-compose
- ebooks-manager
- home
- home-automation
- home-lab
- home-media
- home-media-server
- https
- jackett
- letsencrypt
- nginx-manager
- nginx-proxy
- oauth-proxy
- portainer
- proxmox
- streaming-audio
- streaming-video
- uptime-monitor

## 🎉 Acknowledgments

Thanks to the open-source community for providing these tools and resources. Your contributions make home labs more accessible and enjoyable.

## 🔗 Links

- [GitHub Repository](https://github.com/Aum2bank/home-lab)
- [Releases](https://github.com/Aum2bank/home-lab/releases)

Explore, learn, and enjoy your home lab!