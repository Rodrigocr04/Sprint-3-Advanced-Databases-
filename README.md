Desarrollo e implantación de sistemas de software (Gpo 102)
Sprint 3 (Bases de datos avanzadas) (Miguel) V0 Team
- Diego Espejo
- Diego Cisneros
- Daniel Esparza Arizpe
- Luis Fernando Li Chen
- Rodrigo Castellanos Rodríguez
- 16 de mayo 2025

Tutorial:
Antes de comenzar, asegúrese de contar con lo siguiente:
● SQL Developer instalado
● Docker instalado y en ejecución
● Acceso a su base de datos en Oracle Cloud (OCI)
● Archivo Wallet (.zip) descargado desde la consola de OCI (no debe
descomprimirse)
● Conexión estable a internet

Paso 1: Conectarse a la base de datos en Oracle Desarrollador Nube (OCI)
Abre SQL.
Haga clic en el botón verde “+” para crear una nueva conexión.
Completa los siguientes datos:
● Nombre de conexión: el que prefieres (ej. Oracle Cloud)
● Nombre de usuario: el que prefieres (ej. ADMIN)
● Contraseña: la contraseña correspondiente
● Tipo de conexión: selecciona Cloud Wallet
● Archivo de configuración: selecciona la ruta del archivo .zip del wallet sin
descomprimir
● Servicio: oraclebot_high
Haz clic en Test y luego en Connect.

Paso 2: Instalar Oracle Database Free con Docker
En tu terminal, ejecuta el siguiente comando para lanzar un contenedor de Oracle Free:
● docker run -d -p 1521:1521 -e ORACLE_PASSWORD=
gvenzl/oracle-free:slim-faststart
Esto instalará una base de datos Oracle en tu máquina local accesible en el puerto 1521.

Paso 3: Conectarse a la base de datos Oracle local desde SQL Developer
Una vez que el contenedor esté corriendo, abre SQL Developer y crea una nueva conexión:
● Nombre de conexión: Local Docker
● Nombre de usuario: SISTEMA
● Contraseña: la que define en el comando Docker (si en el comando incluye los < >
debes ponerlos en la contraseña)
● Nombre de host: localhost
● Puerto: 1521
● Selecciona Nombre de servicio y si no funciona, cambia a SID
Haz clic en Test y luego en Connect.
Consejo: El nombre de usuario lo puedes buscar en los registros de Docker a la hora de ejecutarlo, busca algo
similar a esto:
● CONTENEDOR: Restablecer contraseñas de SYS y SISTEMA.
● 2025-05-13 07:55:30 Usuario modificado.

Paso 4: Crear un usuario administrador con privilegios
Conectado como sistema, en el panel de la base de datos:
● Expande el esquema.
● Haz clic derecho en Otros usuarios → Crear usuario.
Llena los campos:
● Nombre de usuario: admin (o el que prefieras)
● Contraseña: adminpass (o el que prefieras)
● En la pestaña Granted Roles, marca todas las opciones necesarias para otorgarle
todos los privilegios.
Haz clic en Aplicar.
Desconéctate de la cuenta system y vuelve a conectarte con el nuevo usuario admin.

Paso 5: Exportar y limpiar el archivo .sql
En SQL Developer, desde tu conexión a la base de datos en OCI:
● Genera una Exportación completa de la base de datos.
● Descargue el archivo .sql.

Abra el archivo .sql en el SQL Worksheet conectado al contenedor Docker y realice la
limpieza:
● Elimina todas las sentencias INSERT INTO (solo necesitamos la estructura, no los
datos)
● Elimina cláusulas TABLESPACE
● Elimina cláusulas COLLATE

Paso 6: Ejecutar el script tabla por tabla
Copia y pega cada sentencia CREATE TABLE (u otros objetos como índices, secuencias)
una por una en el SQL Worksheet.
Ejecuta cada bloque individualmente para asegurarte de que no haya errores.
Verifica que las tablas u objetos se vean correctamente.

Paso 7: Guardar y versionar el archivo final
Una vez confirmado que todo funciona correctamente:
Guarde el archivo limpio con Ctrl + S.
● Nómbralo como V0__base.sql o similar.
Crea una carpeta dentro de tu proyecto llamado:
● sql-migrations/
Coloca el archivo V0__base.sql dentro de esa carpeta.
Este archivo representa la versión base de tu estructura de base de datos para futuros scripts
de migración o control de versiones.