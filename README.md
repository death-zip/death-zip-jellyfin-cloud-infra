# 🎬 Servidor de Streaming Auto-Hospedado con Jellyfin, Docker y Cloudflare Tunnel

[![Estado](https://img.shields.io/badge/estado-en_vivo-brightgreen)](https://media.jarr.cc.cd)
[![Docker](https://img.shields.io/badge/docker-✓-2496ED?logo=docker)](https://www.docker.com/)
[![Cloudflare](https://img.shields.io/badge/cloudflare-tunnel-F38020?logo=cloudflare)](https://www.cloudflare.com/)

> **Repositorio de infraestructura como código (IaC)** para mi servidor de medios personal.  
> **🌐 Proyecto en vivo:** [https://media.jarr.cc.cd](https://media.jarr.cc.cd)  
> **📁 Portafolio:** [https://death-zip.github.io](https://death-zip.github.io)

---

## 📖 ¿Qué es esto?

Este repositorio contiene toda la configuración y los archivos necesarios para desplegar un **servidor de medios completo** (como Netflix o Plex, pero open-source) usando:

- **Jellyfin** como motor de medios.
- **Docker y Docker Compose** para contenerizar y orquestar los servicios.
- **Nginx** como proxy inverso para resolver problemas de CORS y añadir seguridad.
- **Cloudflare Tunnel** para exponer el servicio a internet de forma segura, con HTTPS automático y sin necesidad de abrir puertos en el router.

El objetivo de este proyecto es **demostrar habilidades prácticas en Cloud Engineering y DevOps**: saber contenerizar, orquestar, configurar redes, resolver problemas reales y documentar todo el proceso.

---

## 🏗️ Arquitectura del Sistema

El sistema se compone de 4 capas principales:
Usuario (navegador)
↓
Cloudflare Tunnel (exposición segura, SSL/TLS)
↓
Nginx Proxy (proxy inverso, resuelve CORS)
↓
Contenedor Jellyfin (servidor de medios)
↓
Volumen /media (almacenamiento persistente de películas/series)

### Componentes detallados:

| Componente | Función |
|:---|:---|
| **Cloudflare Tunnel** | Crea un túnel seguro entre tu servidor y Cloudflare, permitiendo acceder a tu servicio desde internet sin abrir puertos. Proporciona certificados SSL automáticos. |
| **Nginx Proxy** | Actúa como intermediario entre el túnel y Jellyfin. Añade cabeceras CORS para que el portafolio web pueda consumir la API de Jellyfin sin bloqueos. |
| **Jellyfin (Docker)** | El servidor de medios en sí. Organiza tu biblioteca de películas, series y música, y permite reproducirlos desde cualquier dispositivo. |
| **Volumen /media** | Almacenamiento persistente donde se guardan los archivos multimedia y la configuración de Jellyfin, para que no se pierdan al reiniciar contenedores. |

---

## 🛠️ Tecnologías Utilizadas

| Tecnología | Propósito |
|:---|:---|
| **Docker** | Contenerización de servicios. |
| **Docker Compose** | Orquestación de múltiples contenedores. |
| **Jellyfin** | Servidor de medios open-source. |
| **Nginx** | Proxy inverso y resolución de CORS. |
| **Cloudflare Tunnel** | Exposición segura a internet con SSL/TLS automático. |
| **Ubuntu 22.04 LTS** | Sistema operativo del servidor (puede ser en WSL2). |
| **Bash** | Scripts y comandos para automatización. |

---

## 📋 Requisitos Previos

Antes de empezar, necesitas tener:

- Un servidor Linux (Ubuntu 22.04 LTS recomendado) o **WSL2** en Windows.
- **Docker** y **Docker Compose** instalados.
- Un dominio (o subdominio) que apunte a Cloudflare (ejemplo: `media.tudominio.com`).
- **cloudflared** instalado (para el túnel).
- Algo de contenido multimedia (películas, series) para probar.

---

## 🚀 Paso a Paso para Desplegar (Instrucciones para cualquier persona)

### 1. Clona este repositorio

```bash
git clone https://github.com/death-zip/death-zip-jellyfin-cloud-infra.git
cd death-zip-jellyfin-cloud-infra
