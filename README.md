# Homelab

Personal homelab running self-hosted services with Docker and Docker Compose.

The setup is organized into separate services, with Caddy handling HTTPS/reverse proxying and Pi-hole providing local DNS.

## Services (Docker)

### Caddy

Reverse proxy and HTTPS entry point for web services.

Used to:

* Route domain names to Docker containers
* Provide HTTPS for internal services
* Keep service ports from being directly exposed where possible

### Jellyfin

Self-hosted media server.

Used for:

* Movies
* TV shows
* Music
* Other personal media

### Minecraft

Self-hosted Minecraft server.

Used to host a private Minecraft server accessible through the local network.

### Nextcloud

Self-hosted file synchronization and collaboration platform.

Used for:

* File storage
* File synchronization
* Personal cloud access
* Sharing files between devices

### Filebrowser

Web-based file manager.

Used to access and manage files stored on the server directly through a browser.

### Immich

Self-hosted photo and video management platform.

Used for:

* Photo and video backup
* Browsing personal media
* Organizing photos and videos
* Accessing the library from other devices

### Ollama + Open WebUI

Local AI platform.

**Ollama** runs local LLMs, while **Open WebUI** provides a web interface for interacting with them.

Used for:

* Running local AI models
* Chatting with local LLMs
* Managing models
* Local AI experimentation

### Pi-hole

Network-wide DNS and ad-blocking service.

Used for:

* Local DNS resolution
* Blocking advertisements and tracking domains
* Providing custom local DNS records

Local services can be assigned internal names such as:

```text
jellyfin.home.arpa
nextcloud.home.arpa
filebrowser.home.arpa
```

Pi-hole resolves these names to the appropriate local server, while Caddy handles the HTTPS reverse proxy.

### Scrutiny

Storage health monitoring system.

Used to:

* Monitor disk health
* Collect S.M.A.R.T. information
* Track drive temperatures
* Detect potential storage problems

### Portainer

Docker management interface.

Used to:

* Manage containers
* Manage Docker images
* Manage networks
* Manage volumes
* View container logs
* Manage Docker Compose stacks

### Monitoring

Monitoring stack based on **Prometheus + Grafana**.

**Prometheus** collects and stores metrics, while **Grafana** provides dashboards and visualization.

Used to monitor:

* Server metrics
* Docker services
* System resource usage
* Service health
* Historical performance

### ComfyUI

Node-based interface for generative AI workflows.

Used for:

* Image generation
* Image processing
* Building custom AI workflows
* Running different generative AI models and pipelines

## Architecture

The services run as Docker containers and are managed using Docker Compose.

The general request flow for web services is:

```text
Client
  |
  v
Pi-hole
  |
  | Local DNS
  v
Caddy
  |
  | HTTPS / Reverse Proxy
  v
Docker Service
```

Monitoring follows a separate flow:

```text
Services / System
       |
       v
   Prometheus
       |
       v
    Grafana
```

Storage and media-related services use the host filesystem where appropriate rather than relying exclusively on Docker-managed volumes.

## Goals

The homelab is primarily focused on:

* Self-hosted services
* Local-first data
* Docker-based deployment
* Centralized HTTPS access
* Local DNS
* Service monitoring
* Personal cloud and media management
* Local AI
* Simple and maintainable infrastructure
