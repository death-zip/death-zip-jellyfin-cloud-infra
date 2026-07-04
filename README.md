# 🎬 Infraestructura Cloud: Servidor Jellyfin + Docker + Cloudflare Tunnel

Este repositorio contiene la infraestructura como código (IaC) de mi servidor de medios auto-hospedado. Está diseñado para ser reproducible y escalable.

## 📋 Requisitos previos
- Servidor Linux (Ubuntu 22.04 LTS recomendado)
- Docker y Docker Compose instalados
- Un dominio (o subdominio) apuntado a Cloudflare
- `cloudflared` instalado (opcional, si usas tunnel)

## 🏗️ Arquitectura
```mermaid
graph LR
    A[Usuario] --> B[Cloudflare Tunnel]
    B --> C[Nginx Proxy]
    C --> D[Jellyfin Container]
    D --> E[(Volumen /media)]
