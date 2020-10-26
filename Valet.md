**INSTALAR VALET EN UN MAC NUEVO**

![](media/image1.jpeg){width="2.220472440944882in"
height="2.0393700787401574in"}Laravel Valet es un entorno de desarrollo
para la creación de proyectos Laravel en ordenadores Apple.

Valet instala el servidor web Nginx y PHP. También crea servidores
virtuales para cada proyecto que desarrollemos. Viene a ser la respuesta
para Apple a la herramienta Laragon para entornos Windows, aunque con un
par de diferencias fundamentales:

-   En lugar del servidor Apache, Valet instala Nginx. Este último es
    más ligero y consume menos recursos, aunque tiene algunas
    funcionalidades menos que Apache. Para el desarrollo y prueba de
    proyectos Laravel es ideal.

-   No instala MySQL, lo que deberemos hacer aparte, como veremos en
    este artículo.

Instalar Laravel Valet en un ordenador Mac en el que no se haya
trabajado previamente con Laravel es un proceso sencillo, que se puede
llevar a cabo en unos pocos pasos.

![](media/image2.jpeg){width="5.905555555555556in"
height="3.3222222222222224in"}

**INSTALAR HOMEBREW**

Homebrew es una herramienta que usan los ordenadores de Apple para la
instalación y actualización de otras herramientas más específicas.

Lo primero es asegurar que tengamos Homebrew instalado. Podemos intentar
ver la versión con:

**brew -v**

Si no lo tenemos instalado, nos mostrará un mensaje de error informando
de que no se reconoce **brew** como un comando. Para instalarlo
usaremos:

**/bin/bash -c \"\$(curl -fsSL
https://raw.githubusercontent.com/Homebrew/install/master/install.sh)\"**

![](media/image3.png){width="1.64375in" height="0.9743055555555555in"}Se
nos pide la contraseña de administrador y, durante la instalación se nos
pedirá confirmación pulsando la tecla **Enter**. El ordenador descarga
los paquetes necesarios y los instala. Al finalizar podemos teclear de
nuevo **brew -v** y, esta vez, si se nos muestra la versión.

Si queremos actualizar Homebrew teclearemos:

**brew update**

INSTALAR COMPOSER Y VALET

![](media/image4.png){width="1.8305555555555555in"
height="2.245138888888889in"}El siguiente paso es instalar Composer, el
gestor de dependencias para PHP, así:

**brew install composer**

Nos aseguramos de que ha quedado instalado tecleando:

**composer -v**

Nos debe aparecer un mensaje con la versión de composer.

Ahora usamos Composer para descargar Laravel Valet:

**composer global require laravel/valet**

Ahora debemos asegurarnos de que la ruta de Valet esté en la variable de
entorno **PATH**, con el siguiente comando:

**export PATH=\$PATH:\~/.composer/vendor/bin**

Ahora debemos instalar Valet en el equipo. Lo haremos con:

**valet install**

Podemos asegurarnos de que valet haya quedado correctamente instalado
tecleando:

**valet -v**

Se nos pedirá la contraseña de administrador y se mostrará la versión de
Valet que tenemos disponible.

INSTALAR MySQL

También deberemos instalar MySQL, que es el motor de base de datos que
se usa en una gran mayoría de proyectos de Laravel. Lo haremos con el
siguiente comando:

**brew install mysql**

![](media/image5.png){width="1.669291338582677in"
height="1.669291338582677in"}Y debemos indicarle a nuestro Mac que MySQL
debe ser un servicio del sistema, con el siguiente comando:

**brew services start mysql**

Necesitaremos alguna herramienta de gestión de bases de datos. Yo
recomiendo usar MySQL Workbench. Al instalarlo con MySQL ya instalado
(o, si lo tenemos de antes, al instalar MySQL) se ha creado una conexión
al puerto 3306, con el nombre de usuario root y sin contraseña, que son
los valores por defecto con los que se instala MySQL en nuestro equipo.

EL DIRECTORIO DE DESARROLLO

Debemos crear un directorio en el que alojaremos los proyectos Laravel.
En mi caso lo voy a llamar **www**, y lo alojaré en el escritorio. Con
el prompt de la terminal en mi directorio de usuario, tecleo lo
siguiente:

**mkdir \~/Desktop/www && cd \~/Desktop/www && valet park**

Con esto hago tres cosas: La primera es crear el directorio con el
mandato **mkdir**. A continuación "entro" en el directorio recién creado
con el mandato **cd**. Por último, con el mandato **valet park** le
indico a Valet que marque el directorio en el que estamos (el que hemos
creado) como raíz de los proyectos Laravel. Por lo tanto, cuando creemos
un proyecto Laravel dentro de ese directorio Valet creará el vhost
necesario para poder ejecutar dicho proyecto en el navegador.

![](media/image6.jpeg){width="2.36875in"
height="0.8131944444444444in"}EL INSTALADOR DE LARAVEL

Debemos usar el gestor de dependencias Composer para agregar a nuestro
entorno de trabajo el instalador de Laravel. En la terminal teclearemos:

**composer global require laravel/installer**

Con esto ya debería estar todo preparado. Nos aseguraremos de que el
instalador de Laravel haya quedado bien, tecleando:

**laravel \--version**

Es posible que la respuesta de la terminal sea un descorazonador
**laravel command not found**. Eso ocurre cuando la ruta necesaria no se
ha añadido a la variable de entorno **PATH**. Para añadirla, teclea lo
siguiente:

**export PATH=\~/.composer/vendor/bin:\$PATH**

Esto solo tendrás que hacerlo una vez. Luego ya queda **PATH**
correctamente.

PROBAR QUE VALET FUNCIONA

Ahora deberemos situarnos en el directorio de trabajo que hemos creado
para nuestros proyectos Laravel. Estemos donde estemos en la terminal
podemos teclear lo siguiente:

**cd \~/Desktop/www**

Aquí podemos crear nuestros proyectos Laravel. Si vamos a crear un
proyecto con la última versión del framework, lo podemos hacer así:

**laravel new prueba**

Si queremos crear un proyecto con una versión anterior (una que a mí me
gusta mucho, por ejemplo, es la 5.8) podemos hacerlo así:

**composer create-project laravel/laravel prueba \'5.8.\*\'**

En cualquiera de los dos casos queda creado el proyecto. Para probar que
todo va bien, abrimos el navegador que queramos y tecleamos, en la barra
de direcciones:

**http://prueba.test**

Con esto se nos cargará nuestro proyecto en el navegador.

Anteriormente Valet creaba los vhosts con el TLD **.dev**. Como este fue
adquirido por Google, ahora se crean con **.test**.

ACERCA DE PATH

En este artículo hemos visto dos formas de añadir una ruta a la variable
de entorno **PATH**. Sin embargo, estas tienen un problema. Si cerramos
la terminal y la volvemos a abrir, las rutas añadidas ya no están en
**PATH**, y tendremos que volver a añadirlas, lo cual es un engorro.

En esta sección vamos a ver el modo correcto de añadir rutas a **PATH**,
de forma permanente, es decir, que cada vez que se abra la terminal,
esas rutas estén directamente disponibles, sin tener que añadir o
teclear nada más.

![](media/image7.png){width="2.838582677165354in"
height="1.31496062992126in"}Las rutas que hay en la variable de entorno
podemos verlas tecleando:

**echo \$PATH**

La respuesta de la terminal es una cadena en la que se ven las rutas
separadas entre si por el guarismo "dos puntos" (**:**).

Las rutas están almacenadas en el fichero **/etc/paths**. Lo que tenemos
que hacer es abrir este fichero para editarlo con el siguiente mandato:

**sudo nano /etc/paths**

Se nos pedirá la contraseña de administrador (dado que pretendemos
actuar como tal, al haber tecleado **sudo**). Después se abre el editor
**nano**, y nos carga el fichero deseado. Veremos que contiene las rutas
de la variable **PATH**, cada una en una línea, sin **:**.

Nos vamos al final de la lista y añadimos, en una línea nueva, la ruta
que nos interesa. En el caso de la instalación que estamos haciendo
será:

**/Users/yo/.composer/vendor/bin**

En esta línea de ejemplo, **yo** es el nombre de usuario de nuestra
cuenta en el Mac.

Para salir pulsaremos **\^X** (la tecla **control** y, sin soltarla, la
**x**). Se nos preguntará si queremos grabar los cambios, a lo que
responderemos con la tecla **y**. Se nos ofrece cambiar el nombre al
fichero. Como no deseamos cambiarlo, simplemente pulsamos la tecla
**enter**.

Con esto ya queda redefinido lo que será, a partir de ahora, el
contenido de la variable **PATH**. Sin embargo, debemos reiniciar la
terminal para que los cambios surtan efecto.
