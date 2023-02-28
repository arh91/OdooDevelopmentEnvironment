# OdooDevelopmentEnvironment
En Docker, levanto un contenedor para Odoo y otro para Postgres para la conexión con bases de datos.


Creo un directorio al que he llamado “odooPlugin”, y dentro de dicho directorio creo el archivo “docker-compose.yml”.

En este dockerfile, creo dos contenedores. Uno para odoo, al que he llamado “dam22_odoo”, y otro para la base de datos con postgreSQL, 
al que he llamado “dam22_postgresql”. 
El puerto que he designado para "dam22_odoo" es el 8069, mientras que para "dam22_postgres" utilizaré el 5432.



Luego, abro el terminal, y ya estando situado dentro del directorio odooPlugin, introduzco el siguiente comando: docker-compose up 
Se nos crean los contenedores con odoo y la base de datos.

Una vez creados y arrancados ambos contenedores, el siguiente paso es comprobar que la conexión con la base de datos funciona. 
Para ello, en el menú superior hago click en View ---> Tool Windows ---> Database. Se nos abre un cuadro a la derecha para añadir conexiones, 
ahora hago click en + para añadir nueva conexión. Nos aparece una lista de servidores de bases de datos, en este caso hago click en postgreSQL. 
Ahora se abre un cuadro con varios campos que hay que completar para poder establecer la conexión, como el usuario y contraseña que he elegido para conectarme a postgreSQL, 
el puerto que va a utilizar el contenedor o el nombre de la conexión. También será necesario descargar el driver específico para poder conectar con el servidor de BBDD 
que vayamos a utilizar, en mi caso tengo que descargar el driver para postgreSQL. Una vez que haya rellenado todos los campos y descargado el driver correspondiente, 
hago click en "Test connection". Si todos los datos están correctos, la conexión se realizará con éxito.



A continuación, en la barra de direcciones del navegador, introduzco: localhost:8069 (ya que el puerto designado en mi dockerfile es el 8069) 
Y me redirigirá a la página de configuración de Odoo, donde rellenaré los campos correspondientes y luego click en “Create database”.

