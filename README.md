# 🚀 Proyecto DevOps Nivel 1

Automatización de despliegue y monitoreo de una aplicación Flask usando herramientas modernas como Ansible, Docker, Prometheus, Grafana y simulación de red con GNS3.

---

## 📌 Descripción general

Este proyecto tiene como objetivo construir una infraestructura básica simulada que permita:

- Desplegar automáticamente una aplicación web (Flask) con Docker
- Configurar un sistema de monitoreo completo (Prometheus + Grafana)
- Simular red realista entre servidores con GNS3
- Ejecutar todo desde un servidor central usando Ansible

---

## 🔄 Fases del Proyecto

Este proyecto se desarrolló en varias fases claramente definidas:

### 🔹 Fase 1 – Preparación del entorno
- Creación de las VMs `vm-control` (Ubuntu) y `vm-web` (Rocky Linux)
- Configuración de red simulada con GNS3
- Conectividad entre servidores (SSH, ping)
- Documentación inicial del entorno  

---

### 🔹 Fase 2 – Automatización con Ansible
- Instalación y configuración básica de Ansible en `vm-control`
- Inventario Ansible y verificación de conexión remota  
<img width="739" height="196" alt="Screenshot 2025-07-23 104933" src="https://github.com/user-attachments/assets/1de6e264-4371-4d26-b641-3cd8a2a8fee6" />


---

### 🔹 Fase 3 – Despliegue de la aplicación Flask
- Clonado desde GitHub usando token
- Despliegue con Docker Compose desde playbook Ansible
- Validación del servicio Flask (http://vm-web:5002)  
<img width="1362" height="684" alt="Screenshot 2025-07-23 105220" src="https://github.com/user-attachments/assets/8eb4f60b-dad6-48b6-9b4b-86c28b9d7b30" />

---

### 🔹 Fase 4 – Sistema de monitoreo
- Instalación y configuración de Prometheus, Grafana, Node Exporter y cAdvisor
- Configuración de targets y dashboards  
<img width="3286" height="1080" alt="Screenshot 2025-07-23 105614" src="https://github.com/user-attachments/assets/b5ecfa9f-2f57-468d-bcd2-a16c25225a4d" />


<img width="1360" height="503" alt="Screenshot 2025-07-23 105745" src="https://github.com/user-attachments/assets/c18e064b-1c35-42d2-beb9-a23e67fa9759" />

---

### 🔹 Fase 5 – Documentación y orquestación
- Consolidación del `master_deploy.yml` para ejecutar todo con un solo comando
- Documentación técnica y subida del proyecto a GitHub
- Separación por repositorios: infraestructura, monitoreo y aplicación
  
<img width="861" height="631" alt="Screenshot 2025-07-23 105844" src="https://github.com/user-attachments/assets/8e13afa1-bc5b-4417-ada6-32509cae3589" />

---

## 🧱 Topología general

```
[VM-CONTROL] (Ubuntu 24.04) ─┬─> GNS3 (Cloud1 → Switch)
                             └─> [VM-WEB] (Rocky Linux 9)
```

- `vm-control`: ejecuta Ansible
- `vm-web`: ejecuta Flask, Docker, Prometheus, Grafana
- GNS3 interconecta los nodos como si fueran parte de una red física  
<img width="411" height="356" alt="Screenshot 2025-07-22 222512" src="https://github.com/user-attachments/assets/924c5669-c0a7-40f4-9431-a352a29c71d1" />


---

## 🛠️ Tecnologías utilizadas

- Ansible
- Docker & Docker Compose
- Flask (Python Web App)
- Prometheus
- Grafana
- Node Exporter & cAdvisor
- GNS3
- GitHub

---

## 📁 Estructura del repositorio

```
devops-lvl1/
├── hosts.ini               # Archivo de inventario Ansible
├── deploy_app.yml         # Playbook Fase 3: despliegue de app Flask
├── deploy_monitoring.yml  # Playbook Fase 4: sistema de monitoreo
├── master_deploy.yml      # Playbook maestro (orquesta todo)
└── README.md              # Este documento
```

---

## ⚙️ Requisitos previos

- VMs con IPs fijas en red 192.168.74.0/24
- Acceso SSH funcional desde vm-control hacia vm-web
- Docker y Ansible instalados
- Token de GitHub configurado como variable de entorno `GITHUB_TOKEN`

---

## 🚀 Ejecución

Desde `vm-control`:

```bash
export GITHUB_TOKEN=ghp_tu_token_aqui
ansible-playbook -i hosts.ini master_deploy.yml
```

<img width="861" height="631" alt="Screenshot 2025-07-23 105844" src="https://github.com/user-attachments/assets/a3d2a148-fb2e-4eb6-8e50-3d78cd34c3f5" />


---

## 🌐 Acceso a servicios

- App Flask: http://192.168.74.130:5002
- Prometheus: http://192.168.74.130:9090
- Grafana: http://192.168.74.130:3000 (usuario: admin, contraseña: admin)

---

## 📸 Capturas importantes (resumen)

- 🖼️ `docker ps` mostrando contenedores activos
<img width="1334" height="147" alt="Screenshot 2025-07-23 110031" src="https://github.com/user-attachments/assets/dedc5f5d-2dab-48fb-b19a-e9a0ae36156d" />


- 🖼️ Targets de Prometheus

<img width="1360" height="503" alt="Screenshot 2025-07-23 105745" src="https://github.com/user-attachments/assets/c08fe486-d278-4a65-a4cd-c898731a89be" />


- 🖼️ Dashboard importado en Grafana
<img width="3286" height="1080" alt="Screenshot 2025-07-23 105716" src="https://github.com/user-attachments/assets/6fb56280-41cd-414c-8cc6-f894dfdef5a6" />


- 🖼️ Playbooks ejecutados desde vm-control
<img width="861" height="631" alt="Screenshot 2025-07-23 105844" src="https://github.com/user-attachments/assets/e9b0e76d-a493-4a4a-ad31-4e8c097a4d72" />

---

## 🧪 Simulación de red con GNS3

- Cloud conectado a VMnet
- VM-control y VM-web integradas como nodos externos
- VPCS opcionales para simular usuarios  

<img width="485" height="213" alt="Screenshot 2025-07-23 120457" src="https://github.com/user-attachments/assets/19c5d297-a517-449e-9b28-b1baad8fbbb4" />


---

## 📈 Futuras mejoras

- Agregar Jenkins para pipeline CI/CD
- Automatizar backup y restauración de dashboards
- Migración a Kubernetes en Nivel 2

---

## 👤 Autor

**Misael Vásquez**  
Ingeniero Telemático | Proyecto DevOps con enfoque realista y automatización completa
