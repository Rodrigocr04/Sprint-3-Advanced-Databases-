Tutorial:
Antes de comenzar, asegúrese de haber completado el primer tutorial y tener lo siguiente:
● Una base de datos Oracle local corriendo vía Docker.
● Acceso mediante SQL Developer con un usuario que tenga privilegios suficientes
(por ejemplo, admin).
● Acceso a la carpeta de migraciones en tu proyecto, típicamente llamada:
sql-migrations.

Paso 1: Agregar la columna intereses (ej. a la tabla de usuarios)
Abre SQL Developer y conéctate a tu base de datos local con el usuario adecuado.
Ejecuta el siguiente comando en la hoja de trabajo SQL:
● ALTER TABLE ADMIN.USUARIOS ADD (INTERESES VARCHAR2(100));
Verifique que se ejecute sin errores.

Paso 2: Crear el archivo de migración
Dentro de tu proyecto, abre la carpeta sql-migrations.
Crea un nuevo archivo con el siguiente formato de nombre:
● V1 ___agrega_columna_intereses.sql (reemplaza con la fecha
actual)
Abre el archivo y copia únicamente la sentencia SQL que realizaste.
Ahora cuentas con una primera migración versionada que representa un cambio puntual en
el esquema de tu base de datos. Esta estructura te permite llevar un control ordenado y
reproducible de los cambios realizados a lo largo del desarrollo.