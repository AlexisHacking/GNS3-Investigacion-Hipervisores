![Estado](https://img.shields.io/badge/Estado-Investigación_Completada-green) ![Plataforma](https://img.shields.io/badge/Plataforma-GNS3%20%2B%20Windows11-blue)

# Investigación: GNS3 e Hipervisores (Windows 11)

Este repositorio documenta la investigación y configuración de un entorno de emulación de redes profesional para la carrera de Ingeniería de Ciberseguridad.

## 1. Arquitectura de Virtualización en Windows 11
Para ejecutar laboratorios de red, se habilitó la **Virtualización** en la BIOS/UEFI. 
* **Seguridad**: Se verificó que el "Aislamiento de núcleo" no bloquee los recursos de VirtualBox.
* **VT-x/AMD-V**: Esencial para que el hipervisor acceda directamente al procesador.

## 2. GNS3 VM: El Motor de Simulación
La GNS3 VM es el servidor que ejecuta los nodos de red de manera eficiente.
* **Soporte KVM**: Como se muestra en la captura, el estado es **True**, garantizando aceleración por hardware nativa.

![Evidencia KVM](img/kvm.png)

## 3. Integración con VirtualBox y VMware ESXi
### VirtualBox (Tipo 2)
Se configuró un adaptador **Host-Only** y se activó el **Modo Promiscuo** (Permitir todo) para que el tráfico de Capa 2 sea procesado correctamente por los routers virtuales.

![Captura de Instalación](img/instalacion.png)

### VMware ESXi (Tipo 1)
A diferencia de VirtualBox, ESXi corre directamente sobre el hardware. La conexión se realiza mediante la IP del servidor y el puerto 3080.

## 4. Matriz de Solución de Errores (Troubleshooting)

| Error Detectado | Causa Técnica | Solución Implementada |
| :--- | :--- | :--- |
| **KVM support: False** | Extensiones de virtualización no enviadas a la VM. | Ejecutar `VBoxManage modifyvm "GNS3 VM" --nested-hw-virt on`. |
| **Error puerto 3080** | Firewall de Windows bloqueando la API. | Crear regla de entrada en el Firewall para el puerto 3080. |
| **Sin conectividad** | Modo promiscuo desactivado. | Cambiar adaptador a "Permitir todo" en VirtualBox. |

## 5. Diagrama de Arquitectura
El siguiente esquema muestra la jerarquía de la instalación:

![Diagrama de Red](img/diagrama.png)

---
*Alexis Smith Navarro Luque - SENATI 2026*
