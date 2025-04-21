# Instalación de MySQL en local

Para poder trabajar con bases de datos desde Java, es necesario tener instalado un sistema de gestión de bases de datos (SGBD). En este apartado veremos cómo instalar **MySQL** en un equipo local, una de las bases de datos más utilizadas.

## Opción 1: Instalación con MySQL Installer (Windows)

1. **Descargar el instalador oficial**  
   Visita [https://dev.mysql.com/downloads/installer/](https://dev.mysql.com/downloads/installer/)  
   Elige el **MySQL Installer (Windows x86, 32-bit, MSI Installer)**.

2. **Ejecutar el instalador**  
   Elige la opción *Developer Default* para instalar todos los componentes necesarios (servidor, Workbench, herramientas de línea de comandos).

3. **Configurar el servidor**
   - Elige puerto 3306 (por defecto).
   - Establece una contraseña para el usuario `root`.
   - Crea un nuevo usuario si lo deseas.

4. **Finalizar instalación y abrir MySQL Workbench**
   - El instalador instalará también **MySQL Workbench**, una herramienta visual para gestionar bases de datos.

> ⚠️ Es importante recordar el puerto (por defecto 3306) y la contraseña del usuario `root`, ya que se necesitarán para conectarse desde Java.

## Opción 2: Instalación con XAMPP (más sencilla, útil si también usan PHP)

1. **Descargar XAMPP**  
   Desde [https://www.apachefriends.org/es/index.html](https://www.apachefriends.org/es/index.html)

2. **Instalar XAMPP**
   - Aceptar todos los componentes por defecto.
   - Una vez instalado, abrir el **Panel de control** y arrancar el módulo **MySQL**.

3. **Usar phpMyAdmin para gestionar la base de datos**
   - Desde el navegador, accede a [http://localhost/phpmyadmin](http://localhost/phpmyadmin)
   - Crea bases de datos desde el menú izquierdo.

> XAMPP no instala MySQL Workbench, pero sí un servidor funcional de MySQL y una interfaz web (phpMyAdmin).

## Opción 3: Instalación en Linux (Ubuntu)

```bash
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql
sudo mysql_secure_installation
```

Después de instalar:
```bash
sudo mysql -u root -p
```

## Verificación

Para comprobar que MySQL funciona:

- Abre **MySQL Workbench** (si lo has instalado).
- Conéctate a `localhost`, usuario `root`, y escribe la contraseña definida.
- Si ves el panel principal, ¡todo está funcionando!
