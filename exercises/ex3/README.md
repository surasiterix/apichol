# API Connect Hands-On Labs

## Ejercicio 3: Generar aplicaciones LoopBack e importar APIs

### Prerrequisitos

**Tener instalado el API Connect Toolkit [Ejercicio 1](../ex1)**

**Instalar [cURL](https://curl.haxx.se/). No olvides agregar al _path_ la ruta donde está el ejecutable de cURL**

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

![newdatasource](https://raw.githubusercontent.com/surasiterix/apichol/master/images/ex3/newdatasource.png "New Datasource")

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

1. Colocaremos la ruta y nombre de nuestro swagger: **../swagger.json**
2. Elegiremos el modelo a ser generado: **swagger_api_v1**
3. Seleccionaremos el _data source_ a emplear para nuestro modelo: **db (memory)**
  
![swaggershaping](https://raw.githubusercontent.com/surasiterix/apichol/master/images/ex3/swaggershaping.png "Swagger Shaping")

Con estos pasos hemos asociado la base de datos en nuestro modelo de aplicación.

### Paso 4: Validación de nuestro modelo en API Connect 

El siguiente paso es confirmar que nuestro modelo esté configurado correctamente, para ello emplearemos el editor de APIs de API Connect. Esta herramienta nos presentará la configuración subyacente del modelo así como los _data sources_ registrados. Ejecutemos el siguiente comando para hacer la validación:

```
apic edit
```

En la interfaz veremos nuestra API en el listado. Ahora, accederemos a la pestaña de "Modelos" para ver el modelo asociado a nuestra API

![Models Tab](https://raw.githubusercontent.com/surasiterix/apichol/master/images/ex3/editmodel.png "Models tab")

Hacer click en el modelo `swagger_api_v1`. Esto abrirá una ventana con las propiedades del modelo. En el campo "Data Source", eligiremos de la lista desplegable el valor **"db"**. Bien, ahora presionaremos el ícono salvar que se ubica en la esquina superior derecha. Al recibir la confirmación de que se han salvado los cambios, cerraremos la ventana del navegador. Tabién hará falta terminar el proceso al ejecutar `apic edit` (Usemos `ctrl + c`)

![New Datasource](https://raw.githubusercontent.com/surasiterix/apichol/master/images/ex3/setdatasource.png "New Datasource")

Excelente! Ahora escribiremos el código de nuestra API. Para ello, veremos los archivos que componen el controlador de la API. Ejecutemos el siguiente comando:

```
dir server\models\*

```

Veremos que hay dos archivos:

1. swagger-api-v-1.js: Define la lógica de implementación de la API. En este caso es un _stub_ generado.
2. swagger-api-v-1.json: Define las meta propiedades del modelo. En este caso fue generado en el paso 3

Para acelerar el paso en nuestra labor de implementación, utilizaremos del ejercicio una implementación ya avanzada. Copiemos el archivo **swagger-api-v-1.js.uncommented** con una implementación parcial del controlador.

```
copy ..\..\swagger-api-v-1.js.uncommented server\models\swagger-api-v-1.js
```

Una vez reemplazado el archivo, tendremos disponible la implementación parcial de 4 métodos para nuestra API

- **GET** y **POST** on  `/mac`
- **GET** y **DELETE** `/mac/{macId}`
 
 Te invito a que le des una mirada a la versión comentanda del controlador en el directorio del ejercicio (`../swagger-api-v-1.js.commented`) para que puedas contrastar los cambios de la implementación que estamos usando.
 
### Paso 5: Ejecutemos nuetra primera API! 
 
Ahora podremos todo junto. Levantemos el _runtime_ de nuestra API para verla en acción:

```
node .
```

Una vez arriba, abriremos una nueva ventana de comandos para generar transacciones a nuestra API. Para ello ejecutaremos los siguientes comandos

```
curl -X POST -H "Content-Type: application/json" -d "{\"organization\":\"IBM Corporation\",\"hex\":\"74:99:75\",\"base16\":\"749975\"}" "http://localhost:3000/api/api/v1/mac"
curl -X POST -H "Content-Type: application/json" -d "{\"organization\":\"IBM Corporation\",\"hex\":\"00:09:6B\",\"base16\":\"00096B\"}" "http://localhost:3000/api/api/v1/mac"
```

Si todo salió bien, debería verse la siguiente respuesta de ejecutar ambos comandos

![Successful Post](https://raw.githubusercontent.com/surasiterix/apichol/master/images/ex3/successfulpost.png "Successful Post")

Ahora haremos una prueba para consultar el registro asociado al ID=2. Usaremos nuestro navegador empleando esta URL 
While it continues to run, let's now fetch a record associated with an ID=2.  Navigate your browser to http://localhost:3000/api/api/v1/mac/2

Excelente! Logramos crear nuetra primera API funcional, creamos registros usando POST e hicimos una consulta usando GET. Buen trabajo!

###Resumen del ejercicio

Hemos realizado un paseo por el proceso para crear una API REST, usando Loopback, a través de una especificacion OpenAPI (swagger). Aplicamos las modificaciones para incorporar una base de datos y modificar el controlador de nuestra aplicación para implementar algunos métodos.

En el [ejericio 4](../ex4) aprenderemos a crear y poblar una base de datos MySQL para que, en los siguientes ejercicios, implmentemos las operaciones CRUD de nuestra API.
