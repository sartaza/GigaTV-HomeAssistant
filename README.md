# GigaTV-HomeAssistant
Transforma tu GigaTV HD870 (S905X) en un servidor profesional de Home Assistant Supervised. Este proyecto detalla la migración a eMMC con Armbian, instalación de Docker, backups en la nube y configuración de acceso remoto seguro. Una guía completa para reciclar hardware y crear el cerebro de tu hogar inteligente con bajo consumo y alta estabilidad.
🚀 Manual: Servidor Home Assistant en GigaTV (S905X)

Este manual detalla cómo reciclar un Android TV Box GigaTV HD870 4K para convertirlo en un servidor de hogar inteligente de bajo consumo y alta disponibilidad.
🛠️ Especificaciones Técnicas

    Hardware: GigaTV HD870 (Procesador Amlogic S905X).

    Sistema Operativo: Armbian (Debian) instalado en la eMMC interna.

    Plataforma: Home Assistant Supervised (Docker).
    📖 Manual: Servidor Home Assistant en GigaTV (S905X)
    
🏗️ Parte 0: Instalación del Sistema Operativo (Armbian)

El GigaTV requiere un "punto de entrada" mediante tarjeta SD antes de pasar el sistema a la memoria interna (eMMC).

    Descarga de la Imagen: Busca la imagen de Armbian para Amlogic S905X (arquitectura arm64). Se recomienda Debian 12 (Bookworm) para asegurar compatibilidad con Docker.

    Quemado de la SD: Usa BalenaEtcher en una microSD de al menos 16GB (Clase 10).

    Configuración del DTB (Vital): * Abre la SD en tu PC y ve a /dtb/amlogic/.

        Localiza el archivo para S905X (ej: meson-gxl-s905x-p212.dtb).

        Edita el archivo uEnv.txt en la raíz de la SD y asegúrate de que la línea dtb_name apunte a ese archivo.

    Primer Arranque: * Introduce la SD en el GigaTV.

        Introduce un palillo en el puerto AV (botón reset oculto), mantén presionado y conecta la alimentación. Yo lo he reiniciado por ADB: Para un reinicio normal del sistema operativo: adb reboot.
Para ir al modo de recuperación: adb reboot recovery.
Para ir al modo bootloader (fastboot): adb reboot bootloader

        Suelta cuando veas el logo de Armbian.

⚙️ Parte 1: Configuración Inicial de Armbian

    Credenciales por defecto: Usuario: root | Password: 1234 (el sistema pedirá cambiarla).

    Migración a eMMC: Una vez estable, ejecuta el comando armbian-install para pasar el sistema de la SD a la memoria interna del GigaTV.

🚀 Parte 2: Despliegue de Home Assistant y Add-ons

Tras instalar Home Assistant Supervised, ve a Ajustes > Complementos e instala estos pilares:

    File Editor: Para editar configuraciones YAML desde el navegador.

    Samba Share: Acceso a las carpetas del servidor desde Windows/Mac como disco en red.

    Google Drive Backup: Copias de seguridad automáticas en la nube.

    HACS (Community Store): La tienda "no oficial" para integraciones avanzadas.

        Instalación: cd /usr/share/hassio/homeassistant && wget -O - https://get.hacs.xyz | bash -

🌐 Parte 3: Configuración de Red y Acceso Externo (Router ZTE)

Para que el sistema sea estable y accesible desde el móvil fuera de casa, configuramos el router:
🏠 Red Local (DHCP Binding)

Evita que el GigaTV cambie de IP interna.

    Ubicación: Local Network > DHCP Server > DHCP Binding.

    Configuración: Vincula la MAC del GigaTV (ej: d0:76:58:48:46:f7) a la IP 192.168.1.100.

    Tip: Si da error "Invalid operation", apaga el GigaTV unos segundos para que el router libere la IP antigua y vuelve a intentar.

🌎 Acceso Exterior (Port Forwarding)

Abre la "puerta" para entrar desde internet.

    Ubicación: Internet > Security > Port Forwarding.

    Regla: Crea un "New Item" con el nombre HomeAssistant.

    Protocolo: TCP.

    Puertos: WAN Port 8123 -> LAN Host Port 8123.

    IP Destino: 192.168.1.100.

📖 Glosario Rápido de Red

    MAC Address: El DNI físico de tu GigaTV (No cambia).

    IP Local: La dirección interna (ej: 192.168.1.100).

    IP Pública: Tu dirección en Internet.

    Puerto 8123: El "timbre" al que llama Home Assistant.

🛡️ Seguridad Final

Una vez abierto el acceso externo, es obligatorio:

    Tener una contraseña robusta.

    Activar el MFA (Doble factor de autenticación) en tu perfil de Home Assistant.
