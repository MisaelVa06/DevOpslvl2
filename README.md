## Proyecto DevOps Nivel 1 – Infraestructura Automatizada con Ansible

Este proyecto consiste en crear una infraestructura DevOps simulada de dos servidores Linux virtuales conectados en red a través de GNS3, donde uno actúa como nodo de control (con Ansible instalado) y el otro como servidor gestionado (donde se automatizan tareas como la instalación de herramientas y Docker).

---

## Objetivo General

Desarrollar una infraestructura automatizada local para practicar conceptos esenciales de DevOps utilizando:

- Máquinas virtuales Linux.
- Red virtual simulada con GNS3.
- Automatización con Ansible.
- Preparación de servidores para despliegue con Docker.

---

## Infraestructura utilizada

- **`vm-control`** (Ubuntu Server):
  - Rol: Nodo controlador
  - Herramientas: Ansible, claves SSH
- **`vm-web`** (Rocky Linux 9):
  - Rol: Servidor gestionado
  - Automatización: Instalación de Docker y utilidades

---

## Herramientas y tecnologías

| Componente     | Tecnología               |
|----------------|--------------------------|
| Virtualización | VMware Workstation       |
| Red simulada   | GNS3 (VMnet1 / VMnet8)   |
| Automatización | Ansible                  |
| Sistema base   | Ubuntu Server + Rocky    |
| Contenedores   | Docker CE (instalado)    |

---

## Estructura del proyecto
devops-nivel1/

    ├── hosts.ini # Archivo de inventario Ansible 
    ├── basic_playbook.yml # Playbook para configurar vm-web 
    └── README.md # Este documento
 
---

## Requisitos para ejecución
1. Conexión SSH sin contraseña desde vm-control hacia vm-web.
2. Usuario remoto (ansible) debe tener privilegios sudo (con o sin contraseña).
3. Ansible instalado en vm-control:

       sudo apt install ansible -y

## Cómo ejecutar
Desde vm-control, dentro del proyecto:

       ansible-playbook -i hosts.ini basic_playbook.yml

Si el usuario remoto requiere contraseña para sudo, usa:

       ansible-playbook -i hosts.ini basic_playbook.yml -K
