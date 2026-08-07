# Write-up: Creación de ambiente de trabajo — Desarrollo de Software Seguro

**Autor:** Rodrigo Perdomo

**Fecha:** 7 de agosto de 2026

Este documento describe, paso a paso, el armado del ambiente de pruebas de aplicaciones utilizado en las prácticas de la materia: una máquina virtual Kali Linux con Burp Suite, Visual Studio Code y Docker, sobre la cual se ejecutan OWASP Juice Shop y crAPI en contenedores, y se configura la interceptación de tráfico HTTP/HTTPS con FoxyProxy y el certificado CA de Burp.

> **Disclaimer:** la redacción de este documento es propia. La organización del material —estructura de directorios, nomenclatura de archivos y disposición de las capturas de pantalla— fue realizada con la asistencia de una herramienta de IA.

## 1. Instalación de una máquina virtual de Kali Linux

Instalación de Kali Linux como máquina virtual en VMware Fusion, desde la descarga/importación de la imagen hasta tener el sistema operativo funcionando.

**1.1** Ventana del VMware.
![1.1](01-instalacion-kali-linux/1.1.jpeg)

**1.2** Crear nueva máquina virtual.
![1.2](01-instalacion-kali-linux/1.2.jpeg)

**1.3** Elegir la imagen.
![1.3](01-instalacion-kali-linux/1.3.jpeg)

**1.4** Confirmar la elección de la imagen.
![1.4](01-instalacion-kali-linux/1.4.jpeg)

**1.5** Asignar el sistema operativo correspondiente a la imagen.
![1.5](01-instalacion-kali-linux/1.5.jpeg)

**1.6** Revisión de recursos: me parece poco disco, poca memoria y poco CPU, hay que cambiarlo.
![1.6](01-instalacion-kali-linux/1.6.jpeg)

**1.7** Cambiar memoria y procesador.
![1.7](01-instalacion-kali-linux/1.7.jpeg)

**1.8** Aumentar número de núcleos.
![1.8](01-instalacion-kali-linux/1.8.jpeg)

**1.9** Aumentar la cantidad de memoria.
![1.9](01-instalacion-kali-linux/1.9.jpeg)

**1.10** Elegir instalación gráfica para más placer.
![1.10](01-instalacion-kali-linux/1.10.png)

**1.11** Sistema en inglés.
![1.11](01-instalacion-kali-linux/1.11.png)

**1.12** Location USA, indiferente para el caso de uso.
![1.12](01-instalacion-kali-linux/1.12.png)

**1.13** Teclado en inglés, tal como en mi máquina física.
![1.13](01-instalacion-kali-linux/1.13.png)

**1.14** Selección de hostname.
![1.14](01-instalacion-kali-linux/1.14.png)

**1.15** Domain name en blanco, no necesario.
![1.15](01-instalacion-kali-linux/1.15.png)

**1.16** Nombre del usuario nuevo.
![1.16](01-instalacion-kali-linux/1.16.png)

**1.17** Username, el que aparece en el login.
![1.17](01-instalacion-kali-linux/1.17.png)

**1.18** Elección de password supersecreta y supersegura.
![1.18](01-instalacion-kali-linux/1.18.png)

**1.19** Configuración de las particiones de disco.
![1.19](01-instalacion-kali-linux/1.19.png)

**1.20** Elección del disco destino.
![1.20](01-instalacion-kali-linux/1.20.png)

**1.21** Una sola partición para el sistema, no son necesarias más particiones para este caso.
![1.21](01-instalacion-kali-linux/1.21.png)

**1.22** Confirmar la partición.
![1.22](01-instalacion-kali-linux/1.22.png)

**1.23** Grabar cambios en el disco.
![1.23](01-instalacion-kali-linux/1.23.png)

**1.24** Instalación de herramientas, por defecto.
![1.24](01-instalacion-kali-linux/1.24.png)

**1.25** Tras finalizar la instalación hay que rebootear.
![1.25](01-instalacion-kali-linux/1.25.png)

**1.26** Primer booteo del sistema nuevo.
![1.26](01-instalacion-kali-linux/1.26.jpeg)

**1.27** Presentación de la pantalla de login.
![1.27](01-instalacion-kali-linux/1.27.jpeg)

**1.28** Clonar repo de pimpmykali porque `apt update` siempre rompe todo. Repositorio en: https://github.com/Dewalt-arch/pimpmykali
![1.28](01-instalacion-kali-linux/1.28.jpeg)

**1.29** Instalar pimpmykali para dispositivo nuevo.
![1.29](01-instalacion-kali-linux/1.29.jpeg)

**1.30** Finalización de la instalación de la herramienta (reboot del sistema recomendado).
![1.30](01-instalacion-kali-linux/1.30.jpeg)

## 2. Instalación del proxy de interceptación (Burp Suite)

Instalación de Burp Suite Community Edition dentro de la máquina virtual Kali Linux.

**2.1** Validar que no exista la herramienta y presentar el comando de instalación.
![2.1](02-instalacion-burp-suite/2.1.jpeg)

**2.2** Validar la instalación.
![2.2](02-instalacion-burp-suite/2.2.jpeg)

**2.3** Iniciar el programa satisfactoriamente.
![2.3](02-instalacion-burp-suite/2.3.png)

## 3. Instalación de Visual Studio Code

Instalación de Visual Studio Code en la máquina virtual Kali Linux.

**3.1** Presentar el comando para descargar el archivo de instalación para la arquitectura correspondiente del sistema.
![3.1](03-instalacion-vscode/3.1.jpeg)

**3.2** Presentar el comando para instalar la herramienta.
![3.2](03-instalacion-vscode/3.2.png)

**3.3** Negar el Microsoft repository porque no es necesario.
![3.3](03-instalacion-vscode/3.3.png)

**3.4** Visual Studio Code instalado correctamente.
![3.4](03-instalacion-vscode/3.4.png)

## 4. Instalación de Docker

Instalación de Docker en la máquina virtual Kali Linux.

**4.1** Validar que la herramienta no esté previamente instalada.
![4.1](04-instalacion-docker/4.1.jpeg)

**4.1.1** No se capturó pantalla de este paso. El comando ejecutado fue:
```
sudo apt install docker.io docker-compose -y
```

**4.2** Confirmar que se eliminen instalaciones previas de Docker; no hay ninguna, así que esto no rompe nada.
![4.2](04-instalacion-docker/4.2.png)

**4.3** Validar la instalación de Docker.
![4.3](04-instalacion-docker/4.3.png)

**4.4** Inicializar los daemon de Docker y validar que se puede levantar un contenedor de prueba.
![4.4](04-instalacion-docker/4.4.jpeg)

## 5. Ejecución de OWASP Juice Shop en ambiente dockerizado

Descarga y ejecución del contenedor de OWASP Juice Shop mediante Docker.

**5.1** Busca en internet una imagen del Juice Shop para Docker.
![5.1](05-juice-shop-dockerizado/5.1.png)

**5.2** Clonar la imagen.
![5.2](05-juice-shop-dockerizado/5.2.png)

**5.3** Finalizar el clonado de la imagen.
![5.3](05-juice-shop-dockerizado/5.3.jpeg)

**5.4** Inicializar la imagen en un nuevo contenedor.
![5.4](05-juice-shop-dockerizado/5.4.jpeg)

**5.5** Validar que el contenedor esté corriendo.
![5.5](05-juice-shop-dockerizado/5.5.jpeg)

**5.6** Validar que se pueda entrar a la app en el navegador.
![5.6](05-juice-shop-dockerizado/5.6.jpeg)

## 6. Ejecución de crAPI en ambiente dockerizado

Descarga y ejecución del contenedor de crAPI (Completely Ridiculous API) mediante Docker.

**6.1** Búsqueda de imagen para Docker de crAPI.
![6.1](06-crapi-dockerizado/6.1.png)

**6.2** Tiene muchas imágenes porque tiene muchos servicios, voy a buscar algo más compacto.
![6.2](06-crapi-dockerizado/6.2.png)

**6.3** Página de OWASP con el GitHub del proyecto.
![6.3](06-crapi-dockerizado/6.3.jpeg)

**6.4** Apartado de la instalación por Docker.
![6.4](06-crapi-dockerizado/6.4.png)

**6.5** Descarga del comprimido con las imágenes.
![6.5](06-crapi-dockerizado/6.5.jpeg)

**6.6** Docker compose del proyecto.
![6.6](06-crapi-dockerizado/6.6.png)

**6.7** Verificación de los puertos para acceder a la aplicación.
![6.7](06-crapi-dockerizado/6.7.png)

**6.8** Validar que se pueda acceder a la aplicación.
![6.8](06-crapi-dockerizado/6.8.png)

**6.9** Validación del segundo front de la app.
![6.9](06-crapi-dockerizado/6.9.png)

## 7. Prueba de visualización del tráfico en el proxy de interceptación

### 7.1 Configuración de FoxyProxy

Configuración de la extensión FoxyProxy en el navegador para enrutar el tráfico hacia el listener de Burp Suite (127.0.0.1:8080).

**7.1.1** Descarga del plugin para Chromium.
![7.1.1](07-configurar-foxyproxy/7.1.1.png)

**7.1.2** Instalación del plugin.
![7.1.2](07-configurar-foxyproxy/7.1.2.png)

**7.1.3** Configuración del plugin.
![7.1.3](07-configurar-foxyproxy/7.1.3.png)

**7.1.4** Configuración del proxy para el navegador.
![7.1.4](07-configurar-foxyproxy/7.1.4.png)

**7.1.5** Validar que exista en el listado de proxies.
![7.1.5](07-configurar-foxyproxy/7.1.5.png)

### 7.2 Instalación del certificado CA de Burp

Instalación del certificado CA generado por Burp Suite en el navegador, y verificación de la interceptación de tráfico HTTPS (en este caso, contra OWASP Juice Shop).

**7.2.1** Validación del proxy del Burp para que encaje con el del Foxy.
![7.2.1](08-instalar-certificado-burp/7.2.1.png)

**7.2.2** Descarga del certificado para el navegador.
![7.2.2](08-instalar-certificado-burp/7.2.2.png)

**7.2.3** Archivo de descarga.
![7.2.3](08-instalar-certificado-burp/7.2.3.png)

**7.2.4** _(pendiente de descripción)_
![7.2.4](08-instalar-certificado-burp/7.2.4.png)

**7.2.5** Instalación en Chromium del certificado.
![7.2.5](08-instalar-certificado-burp/7.2.5.png)

**7.2.6** Interceptor prendido.
![7.2.6](08-instalar-certificado-burp/7.2.6.png)

**7.2.7** Validación de captura de tráfico entre el host y el contenedor.
![7.2.7](08-instalar-certificado-burp/7.2.7.png)
