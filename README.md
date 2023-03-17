# OdooDevelopmentEnvironment
Creo un directorio al que he llamado “odooPlugin”, y dentro de dicho directorio creo el archivo “docker-compose.yml”.

En este dockerfile, creo dos contenedores. Uno para odoo, al que he llamado “dam22_odoo”, y otro para la base de datos con postgreSQL, 
al que he llamado “dam22_postgresql”. 
El puerto que he designado para "dam22_odoo" es el 8069, mientras que para "dam22_postgres" utilizaré el 5432.

![Captura de pantalla (142)](https://user-images.githubusercontent.com/32130215/221934152-8322c93e-6791-4fc6-a644-f395d6866c5a.png)

![Captura de pantalla (143)](https://user-images.githubusercontent.com/32130215/221934208-a2ed3f0a-7de7-4e6b-a1ad-65597a794f7f.png)



Luego, abro el terminal, y ya estando situado dentro del directorio odooPlugin, introduzco el siguiente comando: docker-compose up 
Se nos crean los contenedores con odoo y la base de datos.

Una vez creados y arrancados ambos contenedores, el siguiente paso es comprobar que la conexión con la base de datos funciona. 
Para ello, en el menú superior hago click en View ---> Tool Windows ---> Database. Se nos abre un cuadro a la derecha para añadir conexiones, 
ahora hago click en + para añadir nueva conexión. Nos aparece una lista de servidores de bases de datos, en este caso hago click en postgreSQL. 
Ahora se abre un cuadro con varios campos que hay que completar para poder establecer la conexión, como el usuario y contraseña que he elegido para conectarme a postgreSQL, 
el puerto que va a utilizar el contenedor o el nombre de la conexión. También será necesario descargar el driver específico para poder conectar con el servidor de BBDD 
que vayamos a utilizar, en mi caso tengo que descargar el driver para postgreSQL. Una vez que haya rellenado todos los campos y descargado el driver correspondiente, 
hago click en "Test connection". Si todos los datos están correctos, la conexión se realizará con éxito.

![Captura de pantalla (144)](https://user-images.githubusercontent.com/32130215/221934450-0d05079a-617c-4ee5-a8bc-4a255a611fac.png)


A continuación, en la barra de direcciones del navegador, introduzco: localhost:8069 (ya que el puerto designado en mi dockerfile es el 8069) 
Y me redirigirá a la página de configuración de Odoo, donde rellenaré los campos correspondientes y luego click en “Create database”.

![Captura de pantalla (145)](https://user-images.githubusercontent.com/32130215/221935834-f1211473-e855-4c46-aea4-f3d3ee86522e.png)


Ahora abrimos Visual Studio Code, y en la extensión de Docker consultamos la lista de contenedores creados en nuestro equipo.
Buscamos los contenedores "dam22_odoo" y "dam22_postgresql". Como ya los tenemos funcionando, nos situamossobre "dam22_odoo" y hacemos click en "Attach a Shell".

![Captura de pantalla (163)](https://user-images.githubusercontent.com/32130215/225894260-9a7b500e-58f5-4748-ab83-1916ba5a0e92.png)

Se nos abrirá un terminal para trabajar dentro del contenedor.

Luego si hacemos click sobre el contenedor dam22_odoo y seleccionamos "Attach Visual Studio Code", se nos abrirá una interfaz dentro del contenedor Docker (que obviamente el aspecto y componentes de esa interfaz será distinto al de la interfaz de inicio de VisuaL Studio).

Vamos a la ruta mnt/extra-addons y tecleamos el siguiente comando:
odoo scaffold dam21 .

![Screenshot from 2023-03-14 10-00-36](https://user-images.githubusercontent.com/32130215/225902153-f231ef67-049e-4357-9e17-2f5bb3e28bf7.png)


En donde dam21 es el nombre del módulo que queremos crear. El punto que aparece al final hace referencia al directorio actual en el que nos encontramos (extra-addons).
Con este comando nos genera la estructura de archivos del nuevo módulo dentro de nuestro contenedor.

De entre los archivos que se generan aparece el manifest.py, donde podremos configurar algunas propiedades asociadas al módulo creado.
Éste es el aspecto que tendría un __manifest.py__

![Screenshot from 2023-03-14 10-03-55](https://user-images.githubusercontent.com/32130215/225903426-dfe57efc-f993-422e-9b6f-546cfcf2541b.png)


Dentro del contenedor de Odoo, tecleamos el siguiente comando:

![Screenshot from 2023-03-14 10-30-42](https://user-images.githubusercontent.com/32130215/225904059-71173d1d-735e-4afa-9afd-38df21a1247a.png)

Donde:

-u significa update. Actualiza el módulo correspondiente y sus componentes (si el módulo no existe entonces lo crea).
dam21 es el nombre del módulo que queremos crear.
odoodb es el nombre de la base de datos adonde queremos guardar el modulo.
db es el nombre del servicio (el que le dimos en nuestro docker-compose.yml)
odoo (después de -r) es el nombre de usuario (consultar el docker-compose).
Odoo (después de w) es el nombre de usuario (consultar el docker-compose).



En el fichero __manifest.py__ es donde podemos cambiar las propiedades del módulo.

Cada vez que cambiemos alguna propiedad debemos volver a ejecutar de nuevo el comando: 

bd odoo -u dam21 -d odoodb –dbhost=db -r odoo -w odoo

