# GigaTV-HomeAssistant
Transforma tu GigaTV HD870 (S905X) en un servidor profesional de Home Assistant Supervised. Este proyecto detalla la migración a eMMC con Armbian, instalación de Docker, backups en la nube y configuración de acceso remoto seguro. Una guía completa para reciclar hardware y crear el cerebro de tu hogar inteligente con bajo consumo y alta estabilidad.
🚀 Manual: Servidor Home Assistant en GigaTV (S905X)

Este manual detalla cómo reciclar un Android TV Box GigaTV HD870 4K para convertirlo en un servidor de hogar inteligente de bajo consumo y alta disponibilidad.
🛠️ Especificaciones Técnicas

    Hardware: GigaTV HD870 (Procesador Amlogic S905X).

    Sistema Operativo: Armbian (Debian) instalado en la eMMC interna.

    Plataforma: Home Assistant Supervised (Docker).

🏗️ Fases del Proyecto
1. Preparación y S.O.

    Instalación de Armbian mediante tarjeta SD.

    Migración del sistema a la memoria eMMC para mayor velocidad y fiabilidad (evitando fallos de tarjetas SD).

    Instalación de dependencias de Docker y AppArmor.

2. Despliegue de Home Assistant

    Instalación del Supervisor para tener control total de los Add-ons.

    Configuración de Google Drive Backup: Imprescindible para no perder datos.

    Instalación de Samba Share y File Editor para gestionar archivos desde el PC.

🌐 3. Configuración de Red (Especial Router ZTE)

Para acceder desde fuera de casa, hemos configurado el router ZTE:

    IP Estática (DHCP Binding): Asignar una IP fija (ej. 192.168.1.100) para que el servidor siempre esté en el mismo sitio.

    Port Forwarding: Abrir el puerto 8123 TCP hacia la IP del GigaTV.

    💡 Tip de Experto: Si el router da error "Invalid operation", apaga el GigaTV un momento para liberar la IP dinámica antes de fijarla.

🔒 Seguridad y Acceso Remoto

    Acceso verificado: Acceso externo funcional vía IP Pública.

    Próximo paso: Implementar DuckDNS para acceso mediante nombre de dominio seguro.

    Protección: Activación de MFA (Autenticación de dos factores) para el usuario principal.

📦 Gestión de la Comunidad (HACS)

Para instalar la tienda de la comunidad (HACS) en este sistema:
Bash

cd /usr/share/hassio/homeassistant
wget -O - https://get.hacs.xyz | bash -

📝 Nota del autor

"Este proyecto demuestra que no hace falta comprar hardware caro para tener una casa inteligente. Un equipo que iba a la basura se ha convertido en el cerebro de mi hogar."
