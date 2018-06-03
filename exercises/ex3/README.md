# API Connect Hands-On Labs

## Ejercicio 3: Generar aplicaciones LoopBack e importar APIs

### Prerrequisitos

**Tener instalado el API Connect Toolkit [Ejercicio 1](../ex1)

**Asegúrate que estés en el directorio correcto para el ejercicio ("ex3")**

```
cd <Ruta al laboratorio>\apichol\exercises\ex3
```

### Sumario del ejercicio

En este  ejercicio haremos:

1. Cómo crear una apliación usando LoopBack
2. Cómo consumir especifiaciones OpenAPIs para dar forma al comportamiento a nuestra aplicación LoopBack
3. Cómo implementar el comportamiento básico alrededor del diseño de la API


### Paso 1: Crear una [API LoopBack](https://console.bluemix.net/docs/services/apiconnect/creating_apis.html#create_lb_api)

Primero construiremos un directorio para nuestro proyecto de API

```
mkdir loopbackapp
```
Ahora, accedamos al direcotrio creado

```
cd loopbackapp
```

Ahora construiremos nuestra aplicación usando API Connect, ejecutemos el siguiente comando

```
apic loopback
```

Configuraremos nuestra aplicación usando la opción *Empty-server*

![empty server](https://raw.githubusercontent.com/surasiterix/apichol/master/images/ex3/emptyserver.png "Empty Server")

Estos pasos han creado el esqueleto de nuestra aplicación LoopBack. Ahora crearemos una base de datos en memoria. Esta base de datos nos ayudará a probar nuestra aplicación.

### Paso 2: Crear un conector a base de datos 

Ejecutaremos el siguiente comando:

```
apic create --type datasource
```
Los pasos para configurar el *dataosource* son los siguientes:

1. Nombre del datasource: **db**
2. Conector para la base de datos: **In-memory db**
3. window.localStorage key for persistence: Presiona Enter
4. Full path for file persistence: Persiona Enter

Esto gernerará las especificaciones necesarias para configurar la base de datos a nuestra aplicación LoopBack

![newdatasource](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex3/newdatasource.png "New Datasource")

### Paso 3: Carga del Swagger para nuestra API 

Ahora, copiaremos la especificación swagger que trabajamos en el [ejercicio 2](../ex2)

```
copy ..\..\..\ex2\macreduce.mybluemix.net.json ..\swagger.json
```

Ejecutar el siguiente comando:

```
apic loopback:swagger
```

Configuraremos nuestro swagger en la aplicación:

1. Enter the swagger spec url or file path: **../swagger.json**
2. Select models to be generated: **swagger_api_v1**
3. Select the data-source to attach models to: **db (memory)**
  
![swaggershaping](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex3/swaggershaping.png "Swagger Shaping")

Con estos pasos hemos asociado la base de datos en nuestro modelo de aplicación.

### Paso 4: Carga del Swagger para nuestra API 

Next, you'll confirm that our datasource is attached to our model using the API Design and Management User interface which exposes concepts such as the underlying API model and registered datasources.  To do this, let's jump into the API Design and Management UI by executing the following command:



```
apic edit
```
This should result in the API Design and Management UI opening within your default web browser.  You'll need to sign in with your Bluemix account and browse to the Models tab ...

![Models Tab](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex3/editmodel.png "Models tab")

and click on our model named `swagger_api_v1`.  This will open the properties view for the model.  Click the dropdown arrow and select the datasource **db**.  Hit the **save icon** in the upper right of the window and then close the browser tab.  You'll also need to break out of the running `apic edit` process within the terminal.

![New Datasource](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex3/setdatasource.png "New Datasource")

Sweet!  We now have a node application with endpoints defined via our OpenAPI specification.  To test, let's fire up the app:

```
node .
```

We'll observe that the application is listening on port 3000.  Using a browser, let's navigate to the following url:  [http://127.0.0.1:3000/api/api/v1/mac](http://127.0.0.1:3000/api/api/v1/mac) .

###Ughh ... a 500 response error.  

![not implemented](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex3/notimplemented.png "not implemented")


###Wait, that makes total sense.  We've defined endpoints via a spec but have not implemented any logic around the behavior of the resources.  Let's tackle that next. 

Kill your running node process within the terminal and locate the LoopBack application's model controller file **swagger-api-v-1.js**

```
ls -al ./server/models/

```

Within this folder, you'll notice two files:

1. swagger-api-v-1.js : defines implementation logic for the generated stub APIs generated
2. swagger-api-v-1.json : defines meta properties about the generated API model

To expedite the logic implementation, a handy uncommented copy of a partially implemented controller file is provided within the ex3 parent folder named **swagger-api-v-1.js.uncommented**.  While in the project folder loopbackapp folder, execute the following command to replace the existing controller with this partial implementation:

```
cp ../swagger-api-v-1.js.uncommented server/models/swagger-api-v-1.js
```

You'll be prompted to overwrite.  Respond with **y** (yes).

This partial implementation enables four (4) of the OpenAPI specification entries for 

- **GET** and **POST** on  `/mac`
- **GET** and **DELETE** `/mac/{macId}`
 
If you're curious, we've also provided for comparison and inspection, a commented copy in the ex3 directory. (`../swagger-api-v-1.js.commented`).  

Let's fire up our Loopback Application based on Swagger once again ... and try to populate it with some data.

```
node .
```
In a separate terminal window, issue the following 2 commands:

```
curl -X POST -H "Content-Type: application/json" -d "{\"organization\":\"IBM Corporation\",\"hex\":\"74:99:75\",\"base16\":\"749975\"}" "http://localhost:3000/api/api/v1/mac"
curl -X POST -H "Content-Type: application/json" -d "{\"organization\":\"IBM Corporation\",\"hex\":\"00:09:6B\",\"base16\":\"00096B\"}" "http://localhost:3000/api/api/v1/mac"
```

If all went well, you should receive a response within your terminal from your node backend API server that looks similar to:

![Successful Post](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex3/successfulpost.png "Successful Post")


While it continues to run, let's now fetch a record associated with an ID=2.  Navigate your browser to [http://localhost:3000/api/api/v1/mac/2](http://localhost:3000/api/api/v1/mac/2)

The result should look similar to this:

![Successful Get](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex3/successfulget.png "Successful Get")

Awesome sauce!  Go ahead and kill the running node process within your terminal and change directories to exercise 5.

###Summary of exericse and next steps

You've now walked through the process of quickly creating a REST API Loopback Application shaped by an OpenAPI (swagger) specification.  You also learned how to modify the generated backend Loopback application to partially implement support for a couple of HTTP method types (GET and POST).
<p>
In [Exercise 4](../ex4) we'll learn how to easily create and populate a MySQL database service instance as a building block towards our ultimate goal of establishing API operations that support Create, Read, Update and Delete (CRUD) methods.
