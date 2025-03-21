### Archivos y Directorios del Sistema Básico

1. **/etc/passwd** – Información de usuarios.
2. **/etc/shadow** – Contraseñas cifradas de usuarios (requiere root).
3. **/etc/group** – Información sobre los grupos.
4. **/etc/hosts** – Resolución estática de nombres.
5. **/etc/hostname** – Nombre del host.
6. **/etc/motd** – Mensaje del día.
7. **/etc/resolv.conf** – Configuración de DNS.
8. **/etc/fstab** – Configuración de montaje de sistemas de archivos.
9. **/etc/issue** – Mensaje de aviso antes del login.
10. **/etc/sudoers** – Permisos de `sudo` (requiere permisos root).
11. **/etc/profile**, **~/.bash_profile**, **~/.bashrc** – Archivos de perfil de bash y variables de entorno.
12. **/etc/skel/** – Archivos predeterminados para nuevos usuarios.
13. **/var/log/wtmp** y **/var/log/btmp** – Historial de logins exitosos y fallidos.

### Configuración de Red y Conexiones

1. **/etc/network/interfaces** – Configuración de red.
2. **/etc/sysconfig/network** – Configuración adicional de red en algunas distribuciones.
3. **/etc/hosts.allow** y **/etc/hosts.deny** – Control de acceso de red.
4. **/proc/net/tcp** y **/proc/net/udp** – Conexiones de red TCP/UDP activas.
5. **/etc/iptables/** o **/etc/ufw/** – Configuración del firewall (`iptables` o `UFW`).

### Archivos de Configuración Web

1. **/etc/nginx/nginx.conf** – Configuración de NGINX.
2. **/etc/apache2/apache2.conf** o **/etc/httpd/httpd.conf** – Configuración de Apache.
3. **/etc/httpd/conf.d/** – Configuración adicional de Apache (en distribuciones basadas en Red Hat).
4. **/var/www/html/** – Directorio raíz de la web para Apache/NGINX (sitios web).
5. **/etc/nginx/sites-available/** y **/etc/nginx/sites-enabled/** – Configuración de sitios en NGINX.
6. **/etc/apache2/sites-available/** y **/etc/apache2/sites-enabled/** – Configuración de sitios en Apache.
7. **/usr/share/nginx/html/** o **/usr/share/apache2/** – DocumentRoot de archivos HTML.
8. **/var/log/apache2/** o **/var/log/httpd/** – Registros de Apache.
9. **/var/log/nginx/** – Registros de NGINX.
10. **/var/log/php-fpm/** – Registros de PHP-FPM (si está instalado).
11. /etc/apache2/sites-enabled/000-default.conf
12. /etc/apache2/sites-enabled/monitors.htb.conf

### Archivos de Configuración de Bases de Datos

1. **/etc/mysql/my.cnf** – Configuración de MySQL/MariaDB.
2. **/etc/postgresql/** – Configuración de PostgreSQL.
3. **/var/lib/mysql/** – Archivos de bases de datos de MySQL/MariaDB.
4. **/var/lib/postgresql/** – Archivos de bases de datos de PostgreSQL.
5. **/etc/mongodb.conf** o **/etc/mongod.conf** – Configuración de MongoDB.
6. **/var/lib/mongodb/** – Directorio de datos de MongoDB.
7. **/etc/redis/redis.conf** – Configuración de Redis.
8. **/var/lib/redis/** – Almacenamiento de datos de Redis.
9. **/etc/cassandra/** – Configuración de Cassandra.
10. **/var/log/mysql/** – Registros de MySQL/MariaDB.
11. **/var/log/postgresql/** – Registros de PostgreSQL.

### Archivos y Directorios de Usuarios

1. **~/.ssh/** – Carpeta de claves SSH de usuario.
2. **~/.ssh/authorized_keys** – Claves SSH autorizadas para el usuario.
3. **~/.ssh/id_rsa** – Clave privada SSH del usuario.
4. **~/.bash_history** – Historial de comandos bash.
5. **~/.mysql_history** – Historial de comandos de MySQL.
6. **~/.viminfo** – Archivo de historial y configuración de Vim.
7. **~/.gitconfig** – Configuración de Git del usuario.
8. **/root/.bash_history** – Historial de comandos de root.
9. **/var/mail/** – Correos electrónicos de usuarios locales.

### Directorios Temporales y de Almacenamiento Temporal

1. **/tmp** y **/var/tmp** – Directorios temporales, comúnmente accesibles.
2. **/dev/shm** – Almacenamiento compartido en memoria.
3. **/run/** – Directorio temporal que se reinicia con el sistema.

### Archivos y Directorios de Contenedores y Virtualización

1. **/var/lib/docker/** – Almacenamiento de datos de Docker.
2. **/etc/docker/daemon.json** – Configuración de Docker.
3. **/var/lib/lxc/** – Directorio de almacenamiento de contenedores LXC.
4. **/var/lib/libvirt/images/** – Imágenes de máquinas virtuales en KVM.
5. **/etc/qemu/** – Configuración de QEMU (para virtualización).

### Archivos de Procesos y Estado del Sistema

1. **/proc/cpuinfo** – Información de la CPU.
2. **/proc/meminfo** – Información de memoria del sistema.
3. **/proc/self/environ** – Variables de entorno del proceso actual.
4. **/proc/[PID]/cmdline** – Comando ejecutado por un proceso específico.
5. **/proc/[PID]/fd/** – Descriptores de archivos abiertos de un proceso.
6. **/proc/sys/kernel/random/uuid** – Generador de UUID del kernel.

### Archivos de Registros y Logs

1. **/var/log/auth.log** o **/var/log/secure** – Registros de autenticación.
2. **/var/log/syslog** o **/var/log/messages** – Registros generales del sistema.
3. **/var/log/dmesg** – Mensajes del kernel.
4. **/var/log/lastlog** – Registro de la última conexión de cada usuario.
5. **/var/log/faillog** – Historial de intentos fallidos de conexión.
6. **/var/log/audit/audit.log** – Registro de auditoría.
7. **/var/log/kern.log** – Registros del kernel.
8. **/var/log/cron** – Registro de tareas programadas (Cron).
9. **/var/log/boot.log** – Registro del proceso de inicio.

### Archivos de Configuración de Tareas Programadas

1. **/etc/crontab** – Tareas programadas del sistema.
2. **/etc/cron.d/** – Directorio de tareas programadas adicionales.
3. **/etc/cron.daily/**, **/etc/cron.weekly/**, **/etc/cron.hourly/** – Directorios para tareas programadas según frecuencia.
4. **/var/spool/cron/crontabs/** – Archivos `crontab` específicos de usuario.

### Archivos de Configuración de Servicios (Otros)

1. **/etc/systemd/system/** – Archivos de configuración de servicios en `systemd`.
2. **/etc/init.d/** – Scripts de inicio en sistemas que usan `init`.
3. **/etc/rc.local** – Script ejecutado al final del arranque.
4. **/etc/rsyslog.conf** – Configuración de syslog (registros).
5. **/etc/logrotate.conf** y **/etc/logrotate.d/** – Configuración de rotación de logs.

### Archivos y Directorios de Certificados y Seguridad

1. **/etc/ssl/certs/** – Certificados SSL instalados.
2. **/etc/ssl/private/** – Claves privadas SSL (requiere permisos).
3. **/etc/pki/tls/certs/** – Certificados en sistemas Red Hat.
4. **/etc/ca-certificates/** – Certificados de autoridades certificadoras (CA).
5. **/etc/gpg/** o **~/.gnupg/** – Configuración y claves GPG del sistema o usuario.