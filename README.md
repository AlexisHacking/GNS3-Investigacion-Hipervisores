# Investigación: GNS3 + Hipervisores (ESXi y VirtualBox)

![Estado](https://img.shields.io/badge/Estado-Investigación%20Completada-green)
![Plataforma](https://img.shields.io/badge/Plataforma-GNS3%20%2B%20Windows11-blue)

## 1. Arquitectura de Virtualización en Windows 11
* **Aislamiento de Núcleo y VBS**: Estas funciones de seguridad de Windows 11 pueden generar conflictos con hipervisores de terceros al usar Hyper-V de forma silenciosa.
* **Activación de VT-x/AMD-V**: Es obligatorio habilitar estas extensiones en la BIOS para permitir que el hardware soporte la virtualización anidada.

## 2. GNS3 VM: El Motor de Simulación
* **KVM (Kernel-based Virtual Machine)**: Es vital que aparezca como "True" para obtener un rendimiento profesional mediante aceleración de hardware nativa.
* **Configuración de Recursos**: Se debe asignar CPU y RAM suficientes (ej. 4GB RAM) sin comprometer la estabilidad del sistema anfitrión Windows 11.

## 3. Integración con VirtualBox (Local)
* **Configuración de Red**: Se requiere un adaptador **Host-Only** para permitir la comunicación entre la GUI de GNS3 y el servidor local.
* **Modo Promiscuo**: Configuración técnica necesaria para permitir el flujo de tráfico de Capa 2 entre las máquinas virtuales.

## 4. Integración con VMware ESXi (Remoto)
* **Arquitectura Cliente-Servidor**: Permite gestionar laboratorios desde una laptop conectada a un servidor ESXi físico remoto.
* **Seguridad en vSwitch**: En ESXi, es obligatorio habilitar el "Modo Promiscuo" y "Cambios de dirección MAC" en las políticas de seguridad del port group.

## 5. Matriz de Solución de Errores (Troubleshooting)

| Error Detectado | Causa Técnica | Solución Implementada |
| :--- | :--- | :--- |
| **GNS3 VM: KVM support available: False** | El hipervisor no está pasando las extensiones de virtualización (VT-x/AMD-V) a la VM anidada. | En VirtualBox: Ejecutar `VBoxManage modifyvm "GNS3 VM" --nested-hw-virt on` desde la terminal. |
| **No hay conectividad entre Router y VM** | El Adaptador de Red no está en modo promiscuo o no coincide con el bridge de GNS3. | Cambiar el adaptador a "Generic Driver" o asegurar el Modo Promiscuo en "Permitir todo". |
| **Error de conexión al servidor (Puerto 3080)** | El Firewall de Windows 11 o el Antivirus está bloqueando las peticiones de la API de GNS3. | Crear una regla de entrada en el Firewall para permitir tráfico TCP en los puertos 3080 y 5000-10000. |

---
*Investigación técnica para la implementación de laboratorios avanzados.*
