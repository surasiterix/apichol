# API Connect Hands-On Labs

## Ejercicio 1: Instalar Node.js y el toolkit de API Connect

### Prerrequisitos

Tener pronto el software requerido en la introducción. Prepara un directorio donde quieres que resida el material del laboratorio y clona el repositorio usando Git:

```
git clone https://github.com/surasiterix/apichol
```

Se debió crear un directorio llamado `apichol` donde están todos los contenidos de este laboratorio.

### Asegurate de estar en el directorio correcto

```
cd <ruta>/apichol/exercises/ex1
```

### Sunmario

En este ejercio prepararemos nuestra instancia de Cloud Foundry en IBM Cloud y los servicios de API Connect local.

### Paso 1: Apuntar a nuestra instancia de IBM Cloud

Para región Americas, usamos este comando de la CLI de Cloud Foundry

```
cf api https://api.ng.bluemix.net # to Americas
```
La salida debe lucir como esto

```
Setting api endpoint to https://api.ng.bluemix.net...
OK

api endpoint:   https://api.ng.bluemix.net
api version:    2.92.0
Not logged in. Use 'cf login' to log in.  
```

Hagamos Login a la instancia usando este comando.

```
cf login
```

El resultado debería lucir de esta forma

```
API endpoint: https://api.ng.bluemix.net

Email> <Tu Id de IBM>

Password>
Authenticating...
OK

Targeted org <Nombre de organización>

Targeted space <Nombre del espacio>



API endpoint:   https://api.ng.bluemix.net (API version: 2.92.0)
User:           <Tu Id de IBM>
Org:            <Nombre de organización>
Space:          <Nombre del espacio>
```

En caso de que el espacio esté en blanco, sigamos estas instrucciones; de lo contrario avancemos al paso 2

Listemos los espacios usando este comando

```
cf spaces
```

El resultado debe ser algo como esto

```
Getting spaces in org <Nombre de la Organización> as <IBM Id>...

name
<Nombre del espacio>
```

En caso de no tener espacios en la lista, creemos un espacio con el nombre `dev` usando este comando

```
cf create-space dev
```

La salida debe lucir como esto

```
Creating space dev in org <Nombre de la Organización> as <IBM id>...
OK
Assigning role SpaceManager to user <IBM Id> in org <Nombre de la Organización> / space dev as <IBM id>...
OK
Assigning role SpaceDeveloper to user <IBM id> in org <Nombre de la Organización> / space dev as <IBM id>...
OK

TIP: Use 'cf target -o <Nombre de la Organización> -s dev' to target new space
```

Asignemos el espacio a nuestra instancia de Cloud Foundry usando el comando:

```
cf target -o <Nombre de la Organización> -s <Nombre del espacio en lista o "dev" si tuvista que crearlo>
```

La salida debe lucir como esta:

```
API endpoint:   https://api.ng.bluemix.net (API version: 2.92.0)
User:           <Tu Id de IBM>
Org:            <Nombre de organización>
Space:          <dev o el nombre del espacio listado previamente>
```

### Paso 2: Creemos nuestro primer "Hola Mundo!" (Opcional)

Veamos las aplicationes que tenemos asociadas a nuestro espacio en Cloud Foundry. Ejecutemos este comando

List the apps by issuing the following command.

```
cf apps
```

The output will look something like below.

```
Getting apps in org <Nombre de la Organización> / space <Nombre del espacio en lista o "dev" si tuvista que crearlo> as <Tu Id de IBM>...
OK

No apps found
```
Ahora crearemos nuestro `hola-mundo` usando API Connect. Los pasos a realizar son:

#### Crear aplicación LoopBack

Para ello ejecutaremos el siguiente comando. Seleccionaremos los valores por defecto con excepción de la nota siguiente al comando 

```
apic loopback --name notes
```

En la siguiente pregunta, seleccionaremos la opción marcada con ">". Para ello, mueve el cursor hasta esa opción y pulsa "enter"

```
? What kind of application do you have in mind?
  empty-server (An empty LoopBack API, without any configured models or datasources)
  hello-world (A project containing a controller, including a single vanilla Message and a single remote method)
> notes (A project containing a basic working example, including a memory database)
```

Entremos al directorio de nuestra primera aplicación

```
cd notes
```

Iniciamos nuesrtra aplicación, en este caso se ejecutará local en nuestra instalación de Node.js

```
apic start
```

Asegurate que este corriendo accediendo al siguiente enlace con tu navegador.

```
http://localhost:4001
```

El resultado debe ser un JSON donde se indica la fecha y tiempo arriba de nuestra app. Ejemplo:

```
{"started":"2018-06-01T13:26:33.266Z","uptime":96.596}
```

Ahora accedamos a el editor de APIs de API Connect. Es recomendable que carguemos una variable de entorno para no realizar login. Para Windows, escribamos el siguiente comando

```
set SKIP_LOGIN=true
```
Ahora accedamos al editor de APIs usando este comando

```
apic edit
```

Esta es la GUI para edición de APIs. Más adelante exploraremos esta herramienta, de momento sientete libre de navegar en el editor para familirizarte con la interfaz. 

Ahora, detengamos el editor de APIs con este comando

```
apic stop
```

### Resumen del ejercicio

Felicitaciones! Acabas de aprender como hacer setup de tu ambiente para crear APIs: Referenciar tu instancia de Cloud Foundry en IBM Cloud y usar API Connect local.

En el próximo ejercicio [Ejercicio 2](../ex2) aprenderemos a usar la especificación de OPenAPI (Swagger).
