# Cloud Foundry 101

## Paso 1: Instalar el cliente de Cloud Foundry

Para poder operar con Cloud Foundry (de aquí en adelante "CF"), es necesario instalar el cliente CLI que te va a permitir trabajar con las funciones de uso diario.

Para esto, lo mejor es ir a https://github.com/cloudfoundry/cli#downloads y seleccionar la versión que se ajuste al sistema operativo que estes usando.

Para una mayor comodidad, es mejor que el CLI quede en el PATH para poder ser utilizado de todos lados.

## Paso 2: Conectarse con el API de CF

Usar el CLI requiere conectarse con el API de CF, para que el CLI sepa a dónde enviar los comandos.

Esto se realiza de la siguiente manera:

```
cf api --skip-ssl-validation https://api.54.84.188.243.xip.io
```

Si se conectó bien, vas a ver la siguiente información:

```
Setting api endpoint to https://api.54.84.188.243.xip.io...
OK
```

Ahora, es necesario proveer de credenciales. Esto se logra mediante el comando interactivo `cf login`. Para este workshop, inicialmente usaremos el usuario `workshop_admin`, contraseña `admin`.

## Paso 3: Crear un Space

CF provee una estructura organizacional preparada para soportar organizaciones, espacios y usuarios.
Para crear un espacio, se utiliza el comando `cf create-space`. Probalo y fijate la ayuda que provee el CLI y creá un espacio con tu mismo nombre de usuario, en la *org* **workshop**.

Luego de crear el space, utilizá el comando `cf target` para setear el CLI en la *org* **workshop** y el *space* que acabaste de crear.

## Paso 4: Dar permisos al space

Para lograr esto, es necesario conectarse al CLI como usuario administrador, que es quien permite crear usuarios y administrar roles.
Vamos a usar, en este caso, la variante no interactiva de login de CF, en este caso con el usuario `admin`, contraseña `admin`.

```
cf auth admin "admin"
```

Ahora sí es posible dar permisos:

```
cf set-space-role [tu username] workshop [tu space] SpaceDeveloper
```
Ahora que nuestro usuario tiene ya permisos, se puede hacer deploy de una aplicación.
Pero primero, y antes que nada, autenticate con el tu usuario, puede ser con `cf auth` o `cf login`.

## Paso 5: Deploy de una aplicación

Primero, cloná la aplicación en tu directorio local:
```
git clone https://github.com/eljuanchosf/cf-sinatra-example
cd cf-sinatra-example
```

Hacer un deploy de una aplicación en CF implica utilizar el comando `cf push`. En este caso, vamos a utilizar el siguiente formato `cf push [tu usuario]-app`
Por ejemplo, en caso que tu usuario sea `JoeDoe`, vas a usar:
```
cf push JoeDoe-app
```
Seguramente, CF va a hacer el deploy y va a mostrar que para acceder a la aplicación, podés usar la URL `http://joedoe-app.54.84.188.243.xip.io/`

## Paso 6: Viendo logs

Para ver logs de una aplicación determinada en CF, se utiliza el comando `cf logs`. Ejecutalo, fijate que dice la ayuda y ¡probalo!

## Paso 7: Escalando

Hay dos maneras de escalar aplicaciones en CF: vertical y horizontalmente.
Probá las dos maneras, ambas con el comando `cf scale` (fijate en la ayuda):
* Verticalmente: aumentá el tamaño de memoria de la instancia. ¿Qué sucede?
* Horizontalmente: aumentá la cantidad de instancias de la aplicación. ¿Qué sucede?

Luego, volvé a reducir la cantidad de instancias de la aplicación a una sola instancia.
