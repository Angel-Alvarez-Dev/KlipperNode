# 🚀 **KlipperNode: Control Inteligente para tu Impresora 3D**

**KlipperNode** es una solución moderna y escalable que te permite gestionar tus impresoras 3D desde un servidor remoto basado en **Ubuntu Server** y **Docker**. Con la combinación de **Klipper**, **Moonraker** y **Mainsail**, tendrás el control completo de tus impresoras con una interfaz web segura, accesible desde cualquier lugar.

---

## 🏆 **Objetivo del Proyecto**
1. Implementar un servidor confiable y eficiente para la gestión de impresoras 3D.
2. Simplificar la instalación y configuración mediante contenedores Docker y scripts automatizados.
3. Habilitar acceso remoto seguro con opciones de personalización avanzada.
4. Mantener datos persistentes y configuraciones seguras.

---

## 📌 **Tabla de Contenidos**
- [🏆 Objetivo del Proyecto](#-objetivo-del-proyecto)
- [📋 Requisitos Previos](#-requisitos-previos)
- [📁 Estructura del Proyecto](#-estructura-del-proyecto)
- [🛠️ Instalación Paso a Paso](#️-instalación-paso-a-paso)
- [📖 Configuración de Servicios](#-configuración-de-servicios)
- [🌍 Acceso y Gestión](#-acceso-y-gestión)
- [🔄 Mantenimiento](#-mantenimiento)
- [🤝 Contribuciones](#-contribuciones)
- [🛡️ Licencia](#️-licencia)

---

## 📋 **Requisitos Previos**

### **Hardware**
- 🖥️ **Computadora o Servidor**:
  - Procesador **x86_64** (recomendado)
  - Mínimo 2GB RAM
  - 20GB espacio en disco
  - Conexión USB para las impresoras 3D
- 🌐 **Red**:
  - Conexión Ethernet recomendada
  - IP estática local
  - Puerto 80 y 7125 disponibles

### **Software**
- **Sistema Operativo**: Ubuntu Server 20.04 LTS o superior  
  👉 [Descargar Ubuntu Server](https://ubuntu.com/download/server)
- **Docker** y **Docker Compose**: Última versión estable  
  👉 [Instalar Docker](https://docs.docker.com/engine/install/)

---

## 📁 **Estructura del Proyecto**
```plaintext
KlipperNode/
├── docker-compose.yml      # Configuración de contenedores
├── printer_data/          # Datos persistentes de la impresora
│   ├── config/           # Configuraciones de Klipper
│   ├── logs/            # Registros del sistema
│   └── database/        # Base de datos de Moonraker
├── gcode_files/         # Archivos G-code
└── scripts/             # Scripts de automatización
```

---

## 🛠️ **Instalación Paso a Paso**

### 1. Preparación del Sistema
```bash
# Actualizar el sistema
sudo apt update && sudo apt upgrade -y

# Instalar dependencias necesarias
sudo apt install -y curl git usbutils

# Instalar Docker y Docker Compose
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo apt install docker-compose -y

# Agregar usuario al grupo docker
sudo usermod -aG docker $USER
newgrp docker
```

### 2. Configuración del Proyecto
```bash
# Crear estructura de directorios
mkdir -p KlipperNode/{printer_data,gcode_files}
cd KlipperNode

# Crear docker-compose.yml
nano docker-compose.yml
# [Copiar el contenido del docker-compose.yml proporcionado]

# Identificar puerto USB de la impresora
ls /dev/ttyUSB*
# Modificar docker-compose.yml con el puerto correcto
```

### 3. Despliegue de Servicios
```bash
# Iniciar contenedores
docker-compose up -d

# Verificar estado
docker-compose ps
```

---

## 📖 **Configuración de Servicios**

### Klipper
- Puerto serie: Verificar y ajustar en docker-compose.yml
- Configuración: Disponible en `printer_data/config/`
- Logs: Accesibles en `printer_data/logs/`

### Moonraker
- API REST: Puerto 7125
- Base de datos: Almacenada en `printer_data/database/`
- CORS habilitado para acceso remoto

### Mainsail
- Interfaz web: Puerto 80
- Acceso: `http://<IP_DEL_SERVIDOR>`
- Monitoreo en tiempo real
- Gestión de archivos G-code

---

## 🌍 **Acceso y Gestión**

### Acceso Local
```bash
http://<IP_DEL_SERVIDOR>     # Interfaz Mainsail
http://<IP_DEL_SERVIDOR>:7125 # API Moonraker
```

### Seguridad Recomendada
1. Configurar firewall:
```bash
sudo ufw allow 80/tcp
sudo ufw allow 7125/tcp
sudo ufw enable
```

2. Implementar HTTPS:
- Usar reverse proxy (nginx)
- Configurar certificados SSL
- Implementar autenticación básica

### Acceso Remoto
Opciones recomendadas:
- VPN (OpenVPN, WireGuard)
- Tailscale
- Cloudflare Tunnel

---

## 🔄 **Mantenimiento**

### Actualizaciones
```bash
# Actualizar imágenes
docker-compose pull

# Reiniciar servicios
docker-compose down
docker-compose up -d
```

### Backups
```bash
# Respaldar configuraciones
tar -czf backup_$(date +%Y%m%d).tar.gz printer_data/
```

### Monitoreo
```bash
# Ver logs
docker-compose logs -f

# Estado de contenedores
docker-compose ps
```

---

## 🤝 **Contribuciones**
¡Tu participación es valiosa! 

1. Fork del repositorio
2. Crear rama de características (`git checkout -b feature/AmazingFeature`)
3. Commit de cambios (`git commit -m 'Add: AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abrir Pull Request

---

## 🛡️ **Licencia**
Este proyecto está bajo la licencia [MIT](LICENSE).

---

## 🌟 **Soporte**
Si encuentras útil este proyecto:
- Dale una ⭐ en GitHub
- Comparte con la comunidad
- Reporta issues o bugs
- Contribuye con mejoras

---

### 📞 **Contacto**
- GitHub Issues: Para problemas y sugerencias
- Discussions: Para preguntas y debates
- Wiki: Para documentación extendida

---

*Última actualización: Noviembre 2024*