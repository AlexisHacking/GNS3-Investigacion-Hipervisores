# Investigación: GNS3 e Hipervisores

## 1. Configuración en Windows 11
Para que la virtualización funcione, se debe habilitar en la BIOS. En Windows 11, es importante vigilar el "Aislamiento de núcleo", ya que puede entrar en conflicto con VirtualBox.

## 2. GNS3 VM y Soporte KVM
He logrado configurar la GNS3 VM exitosamente. En la siguiente imagen se confirma que el soporte KVM está en **True**, lo que garantiza un rendimiento profesional.

![Prueba de KVM](img/Prueba%20de%20Rendimiento%20KVM%20True)

## 3. Instalación de la Infraestructura
Se utilizó VirtualBox para importar la GNS3 VM, asegurando que los adaptadores de red estén correctamente vinculados.

![Captura de Instalación](img/Instalación%20de%20GNS3%20VM)

## 4. Matriz de Errores (Troubleshooting)

| Error | Causa | Solución |
| :--- | :--- | :--- |
| KVM en False | Virtualización anidada desactivada | Habilitar VT-x en la configuración de la VM |
| Error Puerto 3080 | Firewall bloqueando GNS3 | Crear regla de entrada en el Firewall |
| Sin conexión | Modo promiscuo desactivado | Activar "Permitir todo" en la red de VirtualBox |
