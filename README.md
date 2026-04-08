# [cite_start]Investigación: GNS3 + Hipervisores (ESXi y VirtualBox) [cite: 2]

[cite_start]![Estado](https://img.shields.io/badge/Estado-Investigación%20Completada-green) [cite: 79]

## [cite_start]1. Arquitectura de Virtualización en Windows 11 [cite: 11]
* [cite_start]**Aislamiento de Núcleo y VBS**: Estas funciones de seguridad de Windows 11 pueden generar conflictos con hipervisores de terceros al usar Hyper-V de forma silenciosa[cite: 13, 49].
* [cite_start]**Activación de VT-x/AMD-V**: Es obligatorio habilitar estas extensiones en la BIOS para permitir que el hardware soporte la virtualización anidada[cite: 14].

## [cite_start]2. GNS3 VM: El Motor de Simulación [cite: 15]
* [cite_start]**KVM (Kernel-based Virtual Machine)**: Es vital que aparezca como "True" para obtener un rendimiento profesional mediante aceleración de hardware nativa[cite: 16].
* [cite_start]**Configuración de Recursos**: Se debe asignar CPU y RAM suficientes (ej. 4GB RAM) sin comprometer la estabilidad del sistema anfitrión Windows 11[cite: 18].

## [cite_start]3. Integración con VirtualBox (Local) [cite: 19]
* [cite_start]**Configuración de Red**: Se requiere un adaptador **Host-Only** para permitir la comunicación entre la GUI de GNS3 y el servidor local[cite: 21].
* [cite_start]**Modo Promiscuo**: Configuración técnica necesaria para permitir el flujo de tráfico de Capa 2 entre las máquinas virtuales[cite: 22].

## [cite_start]4. Integración con VMware ESXi (Remoto) [cite: 23]
* [cite_start]**Arquitectura Cliente-Servidor**: Permite gestionar laboratorios desde una laptop conectada a un servidor ESXi físico remoto[cite: 24].
* [cite_start]**Seguridad en vSwitch**: En ESXi, es obligatorio habilitar el "Modo Promiscuo" y "Cambios de dirección MAC" en las políticas de seguridad del port group[cite: 25].

## [cite_start]5. Matriz de Solución de Errores (Troubleshooting) [cite: 26, 39]

| Error Detectado | Causa Técnica | Solución Implementada |
| :--- | :--- | :--- |
| **KVM support available: False** | [cite_start]Falta pasar las extensiones de virtualización (VT-x) a la VM[cite: 42]. | [cite_start]Ejecutar `VBoxManage modifyvm "GNS3 VM" --nested-hw-virt on`[cite: 42, 47]. |
| **Sin conectividad Router-VM** | [cite_start]El adaptador no está en modo promiscuo o no coincide el bridge[cite: 42]. | [cite_start]Cambiar a "Generic Driver" o activar Modo Promiscuo en "Permitir todo"[cite: 42]. |
| **Error puerto 3080** | [cite_start]El Firewall de Windows 11 está bloqueando la API de GNS3[cite: 42]. | [cite_start]Crear regla de entrada en el Firewall para los puertos TCP 3080 y 5000-10000[cite: 42]. |S# GNS3-Investigacion-Hipervisores
