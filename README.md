# servidor-unversitario-telematica


# 🖥️ Proyecto Final – Servidor Universitario para Telemática

## 📘 Descripción del Proyecto

Este proyecto tiene como objetivo la instalación, configuración y documentación de un servidor Linux funcional, simulado dentro de una máquina virtual. Este servidor integra servicios clave para un entorno universitario como:

- 📦 MySQL para bases de datos
- 🌐 Apache2 con WordPress para el servidor web
- 🌍 Bind9 para DNS
- 📡 isc-dhcp-server para DHCP
- 🔐 SSH para acceso remoto
- 📁 VSFTPD para FTP
- 🛠️ Automatización de tareas con `cron` y respaldo con `rsync`

El trabajo fue realizado por un equipo de cinco estudiantes, cada uno desempeñando un rol específico dentro del desarrollo del proyecto.

---

## 🗓️ Bitácora Semanal (Tareas Realizadas)

| Semana | Actividades |
|--------|-------------|
| Semana 1 | Instalación de Mini OS en live USB |
| Semana 2 | Instalación de MySQL y creación de base de datos `telematica` y tabla `estudiantes` |
| Semana 3 | Instalación de Apache2, PHP y WordPress. Verificación en navegador local |
| Semana 4 | Configuración de Bind9 como servidor DNS |
| Semana 5 | Instalación y configuración del servidor DHCP |
| Semana 6 | Configuración de SSH para acceso remoto y servidor FTP (VSFTPD) |
| Semana 7 | Creación de scripts de backup con `rsync`, programación con `cron`, modificación de GRUB |
| Semana 8 | Revisión final, capturas, solución de errores, documentación y subida a GitHub |

---

## 🧾 Comandos Importantes Utilizados

### 🔧 MySQL

```bash
sudo apt update
sudo apt install mysql-server
sudo mysql_secure_installation
```

```sql
CREATE DATABASE telematica;
USE telematica;

CREATE TABLE estudiantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    edad INT,
    carrera VARCHAR(50)
);

INSERT INTO estudiantes (nombre, apellido, edad, carrera)
VALUES 
('Ana', 'Gómez', 20, 'Telemática'),
('Luis', 'Martínez', 22, 'Informática'),
('Carla', 'Rojas', 21, 'Electrónica');
```

### 🌐 Apache + PHP + WordPress

```bash
sudo apt install apache2 php libapache2-mod-php php-mysql
sudo systemctl start apache2
sudo systemctl enable apache2
```

### 🌍 DNS (Bind9)

```bash
sudo apt install bind9
sudo systemctl enable bind9
sudo systemctl start bind9
```

### 📡 DHCP

```bash
sudo apt install isc-dhcp-server
sudo systemctl enable isc-dhcp-server
sudo systemctl start isc-dhcp-server
```

### 🔐 SSH

```bash
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

### 📁 FTP (VSFTPD)

```bash
sudo apt install vsftpd
sudo systemctl restart vsftpd
```

### 🛠️ Automatización con `cron` y respaldo con `rsync`

**Script:** `/usr/local/bin/backup.sh`

```bash
#!/bin/bash
rsync -av --delete /home /backup/
```

**Cron job diario:**

```bash
sudo crontab -e
# Ejecutar todos los días a las 2:00 am
0 2 * * * /usr/local/bin/backup.sh
```

---

## 👥 Integrantes del Equipo

| Nombre | Rol |
|--------|-----|
| **Roberto Cruz** | Líder del Proyecto / Responsable de Automatización y Backups |
| **Jasmir Alberto** | Responsable de Base de Datos y Conexión desde DBeaver |
| **Alberto Pérez** | Configuración de Red, DHCP y DNS |
| **Denis Pavón** | Configuración del Servidor Web (Apache + WordPress) |
| **Kevin Molina** | no trabajo |

---

## ✅ Estado de los Servicios

Usamos un script para comprobar el estado de todos los servicios:

```bash
#!/bin/bash

SERVICIOS=("mysql" "apache2" "bind9" "isc-dhcp-server" "ssh" "vsftpd" "cron")

for servicio in "${SERVICIOS[@]}"; do
    echo -e "\n🔍 Estado de: $servicio"
    systemctl is-enabled "$servicio" &>/dev/null && echo "➡️  Habilitado" || echo "⛔  No habilitado"
    systemctl is-active "$servicio" &>/dev/null && echo "✅ Activo" || echo "❌ Inactivo"
done
```

---

## 🎓 Conclusión y Recomendaciones

Este proyecto nos permitió adquirir experiencia práctica sobre la instalación, configuración y administración de servicios esenciales en un servidor Linux. Cada miembro pudo desarrollar habilidades específicas y trabajar en conjunto para consolidar un entorno robusto.

**Recomendaciones:**

- Mantener respaldos automáticos y revisarlos regularmente
- Documentar todos los cambios importantes en el servidor
- Usar herramientas gráficas como DBeaver para facilitar la administración
- Mantener el sistema y los servicios actualizados
