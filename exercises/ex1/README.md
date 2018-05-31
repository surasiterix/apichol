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

TIP: Use 'cf target -o raghsrin@us.ibm.com -s dev' to target new space
```

Asignemos el espacio a nuestra instancia de Cloud Foundry usando el comando:

```
cf target -o <IBM Id> -s <Nombre del espacio en lista o dev si lo creaste>
```

La salida debe lucir como esta:

```
API endpoint:   https://api.ng.bluemix.net (API version: 2.92.0)
User:           <Tu Id de IBM>
Org:            <Nombre de organización>
Space:          <dev o el nombre del espacio listado previamente>
```

### Paso 2: Creemos nuestro primer "Hola Mundo!"

List the apps by issuing the following command.

```
cf apps
```

The output will look something like below.

```
Getting apps in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

No apps found
```

Next we will create a simple `hello-world` project using API Connect.

### Create a "hello world" API connect project

Create a Loopback application. Pick the defaults except as noted below.

```
apic loopback --name notes
```

Pick the defaults except for the sample application notes instead of the default option.

```
? What kind of application do you have in mind? notes (A project containing a basic working example, including a memor
y database)
```

Change to the project directory

```
cd notes
```

Start the API connect services locally

```
apic start
```

Ensure the service is running via the command

```
curl -l localhost:4001
```

Which should display how long the service has been running

You can try other options as available in the following command

```
apic --help
```

You can explore further by invoking the following command

```
SKIP_LOGIN=true apic edit
```

This will launch the API connect GUI in the default browser. You will have to override the certificates manually. For now, feel free to wander around. We will take a more formal guided tour in the subsequent exercise.

Finally, you can stop the service as below.

```
apic stop
```

Which should show the service being stopped.

You can clean up by deleting the sub-directory if you prefer.

```
cd ..
rm -rf notes
```

We will dive into API Connect in the subsequent exercises.

### Summary of exercise and next steps

After installing all the prerequisites, we explored how to target a Bluemix/Cloud Foundry instance and use the API connect product locally.

In [Exercise 2](../ex2) we will look at how to use the OpenAPI specification (swagger) editor.

