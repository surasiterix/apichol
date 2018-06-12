# API Connect Hands-On Labs

## Ejercicio 6: Probar, Explorar y desplegar aplicaciones LoopBack

### Prerrequisitos

Este ejercicio requiere de lo siguiente:

**Tener instalado el toolkit de API Connect** del [ejericio 1](../ex1).

**La app de Loopback** del [ejericio 3](../ex3)

**La base de datos Cleardb** del [ejercicio 4](../ex4)

**APIs CRUD** del [ejercicio 5](../ex5)

### Sumario

En este ejercicio veremos el fruto del trabajo hasta ahora realizado. Probaremos nuestras APIs y exploraremos el Swagger generado, para luego, hacer nuestro despliegue en IBM Cloud

### Paso 1: Levantemos el Ambiente

**Importante**: Aseguremos estar en el directorio del ejercicio 3

```
cd <Ruta al laboratorio>\apichol\exercises\ex3
```  

Accedamos al directorio de nuestra aplicación loopback

```
cd loopback\myloopbackapp
```

Iniciemos el toolkit de API Connect empleando este comando

```
set SKIP_LOGIN=false
apic edit
```

Esta vez utilicemos nuestra credencial de acceso a IBM Cloud (También llamado IBM Id). 

Una vez halla cargado el toolkit, levantaremos nuestra aplicación pulsando el botón "Play" ubicado en la parte inferior izquierda. Nuestra aplicación estará arriba una vez veamos "Running..." barra de estado como en la siguiente imagen

![Node Running](../../images/APIC_Noderunning.png)

Como podemos ver, existen dos direcciones: **Gateway** y **Application**. El primero representa la puerta de entrada de nuestras APIs, donde podemos configurar políticas de seguridad para proteger nuestras APIs. El segundo es donde está el _end-point_ de nuestra APIs.

### Paso 2: Exploremos nuestra API

Ahora que está arriba nuestro ambiente, probemos llamar a algunas APIs!

Pulsemos el botón de "Explore" (Compás) en la parte superior derecha. Esto nos mostrará el documento swagger con todos los servicios REST disponibles

![Swagger](../../images/APIC_Swagger.png)

En el swagger podemos ver los servicios creados en el ejericio 3 y en el 5. Ahora probemos los servicios

### Paso 3: Ejecutemos una API

Probemos hacer una consulta de nuestros empleados usando el servicio **GET /Employees**. Antes, precisamos desactivar CORS (Cross-origin Resource Sharing) que es una política de seguridad para evitar que los recursos sean accesibles fuera del dominio definido. Para ello, haremos click en la viñeta "APIs" y seleccionaremos nuestra API.

En el panel izquierdo seleccionaremos "Lifecycle", para luego desactivar la validación CORS.

![Disabling CORS](../../images/APIC_DisablingCORS.png)

Ahora procederemos con la prueba de nuestro servicio. Volvamos a dar click en "Explore" y seleccionemos de los _drafts_ employees.find

Haremos click en el enlace "Try it"



Along the left side, you should see a number of operations for the `Employee` model you created in [exercise 5](../exercises/ex5). Let's try calling a series of these operations.

#### GET /Employees

Let's test retrieving the list of Employees.

Navigate to the operation `GET /Employees`. Along the right side, there is a black section which shows you how to call that operation, provides boiler code, and has a button "Call Operation". Hit the button to call your GET operation.

<img src="SS3.png"  width="800">

You might get a CORS error. Please override the CORS error as suggested in exercise 2. Then, retry the `Call Operation`.

You should see a `200 OK` response, along with a large list of employees in the database!

<img src="SS4.png"  width="300">

#### POST /Employees

Let's test adding an employee to the database.

Navigate to the operation `POST /$Employees` to create a database entry. Scroll down to the "Call Operation" button, enter some data into the Parameters section (or use the `Generate` button), and hit call Operation.

<img src="SS5.png"  width="300">

You should see a `200 OK` response, as well as a response body indicating that the database update has succeeded.

<img src="SS6.png"  width="300">

### Deploy your APIs to IBM Bluemix

Once you're happy with the APIs you've created, you can push them the Bluemix, IBM's PaaS (Platform as a Service).  Bluemix will host your APIs and allow you to graphically manage them.

Start by hitting the Publish button on the top right of the API Designer.

Choose `Add and Manage Targets` and `Add IBM Bluemix target`.

Ensure that the organization is correct -- it should correspond to your Bluemix email.  Choose the `Sandbox` catalog.

<img src="SS7.png"  width="300">

Type a new application name: `EmployeeAPI`. Then hit the `(+)` button, and hit `Save`.

<img src="SS8.png"  width="300">

You've now created a publish target; deploy to it by hitting the `Publish` button and choosing the target you just created.

<img src="SS9.png"  width="300">

Choose both `Publish Application` and `Stage or Publish` products. Hit `Publish`. That's it! Your APIs are now securely pushed to the cloud.

<img src="SS10.png"  width="300">

It may take a few minutes for the application to get started. You can track the status of your application by using the `CF` client that you setup in [Exercise 1](../ex1). Simply run the `cf app EmployeeAPI` command:

```
$ cf app employeeapi
Showing health and status for app employeeapi in org raghsrin@us.ibm.com / space dev as raghsrin@us.ibm.com...
OK

requested state: started
instances: 0/1
usage: 256M x 1 instances
urls: apiconnect-be783035-d8e9-4ceb-b2d7-f16e9340c1d1.raghsrinusibmcom-dev.apic.mybluemix.net
last uploaded: Tue Sep 13 19:06:32 UTC 2016
stack: cflinuxfs2
buildpack: unknown
```

Once the `requested state` is `started`, the application is started and your APIs are being managed by API Connect!

### Summary and next steps

In this exercise we explored, tested and deployed the application to Bluemix.

In the next two exercises, we'll explain how you can test your APIs and create a developer portal so others can consume your APIs.

Next up, Exercise 7: [Explore your deployed APIs with the API Manager on Bluemix](../ex7)
