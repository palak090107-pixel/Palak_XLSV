# Palak_XLSV

### Nextcloud-Based Offline Collaboration System for Real-Time Spreadsheet Editing

## Overview

Palak_XLSV is a self-hosted offline collaboration platform that enables multiple users on the same local network to collaboratively edit Excel spreadsheets in real time without relying on the public internet or third-party cloud services.

The project combines:

* **Nextcloud** for file storage and collaboration
* **Collabora Online** for browser-based spreadsheet editing
* **Docker & Docker Compose** for containerized deployment

The system works entirely on a local Wi-Fi/LAN network and provides a Google Sheets–like experience while keeping all data inside the organization’s infrastructure.

---

## Features

* Real-time multi-user spreadsheet editing
* Fully offline/local network operation
* Self-hosted and secure
* Browser-based access (no client installation required)
* Dockerized deployment using Docker Compose
* Persistent storage using Docker volumes
* Cross-platform deployment (Windows/Linux/macOS)

---

## Technologies Used

| Technology            | Purpose                        |
| --------------------- | ------------------------------ |
| Docker                | Containerization platform      |
| Docker Compose        | Multi-container orchestration  |
| Nextcloud             | File hosting and collaboration |
| Collabora Online      | Real-time document editing     |
| YAML                  | Docker Compose configuration   |
| VirtualBox (Optional) | VM-based deployment            |

---

## System Architecture

```text
+-----------------------+
|   Client Devices      |
| (Browser Access)      |
+-----------+-----------+
            |
            v
+-----------------------+
|    Nextcloud Server   |
|  File Management Hub  |
+-----------+-----------+
            |
            v
+-----------------------+
|   Collabora Online    |
| Spreadsheet Editor    |
+-----------------------+
            |
            v
+-----------------------+
| Docker Volume Storage |
+-----------------------+
```

---

## Project Objectives

* Build a fully self-hosted collaboration system
* Enable simultaneous spreadsheet editing
* Eliminate dependency on public cloud services
* Support offline/local-network-only operation
* Provide reproducible deployment using Docker Compose

---

## Prerequisites

Before running the project, ensure the following are installed:

* Docker Desktop
* Docker Compose
* Git
* Optional: VirtualBox

---

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/palak_xlsv.git
cd palak_xlsv
```

---

### 2. Create `docker-compose.yml`

```yaml
version: '3'

services:
  nextcloud:
    image: nextcloud:latest
    ports:
      - "8080:80"
    volumes:
      - nextcloud_data:/var/www/html
    restart: unless-stopped

  collabora:
    image: collabora/code:latest
    ports:
      - "9980:9980"
    environment:
      - domain=YOUR_LOCAL_IP
      - username=admin
      - password=admin
      - extra_params=--o:ssl.enable=false
    cap_add:
      - MKNOD
    restart: unless-stopped

volumes:
  nextcloud_data:
```

---

### 3. Start the Containers

```bash
docker compose up -d
```

---

### 4. Verify Running Containers

```bash
docker ps
```

---

### 5. Find Your Local IP Address

#### Windows

```bash
ipconfig
```

#### Linux/macOS

```bash
ifconfig
```

---

### 6. Open Nextcloud

In your browser:

```text
http://<host-ip>:8080
```

Example:

```text
http://172.20.10.5:8080
```

---

## Workflow

1. Start Docker Desktop
2. Run `docker compose up -d`
3. Access Nextcloud from browser
4. Upload or create `.xlsx` spreadsheet
5. Open file inside Collabora Online
6. Share local IP with other users
7. Collaborate in real time

---

## Multi-User Collaboration

The system supports:

* Simultaneous editing
* Live cursor tracking
* Shared spreadsheet sessions
* Real-time synchronization

All changes are stored locally on the host machine.

---

## Advantages

* No internet dependency
* Secure local-only data sharing
* Zero licensing cost
* Portable deployment
* Easy scalability
* Familiar spreadsheet interface

---

## Challenges Solved

* Collabora trusted-domain configuration
* Persistent storage management
* Local IP configuration
* Real-time concurrency verification
* Container capability permissions

---

## Future Improvements

* HTTPS/SSL support
* Static IP configuration
* LDAP/Active Directory integration
* Automated backups
* Mobile application support
* Portable VM packaging

---

## Screenshots

Add screenshots here:

```text
/screenshots/dashboard.png
/screenshots/collaboration.png
/screenshots/docker-containers.png
```

---

## Use Cases

* Research labs
* Educational institutions
* Defense/offline environments
* Small organizations
* Secure internal collaboration systems

---

## Conclusion

Palak_XLSV demonstrates that real-time collaborative spreadsheet editing can be achieved completely offline using open-source technologies. By integrating Nextcloud and Collabora Online through Docker Compose, the project delivers a secure, low-cost, and reproducible alternative to public cloud collaboration platforms.

---

## Author

**Palak Sharma**

---

## License

This project is open-source and available under the MIT License.
