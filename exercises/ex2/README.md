# API Connect Hands-On Labs

## Ejercicio 2: Diseñar especificaciones swagger OpenAPI

### Prerrequisitos

**Tener instalado el API Connect Toolkit [Ejercicio 1](../ex1)

**Asegurarte que estés en el directorio correcto para el ejercicio ("ex2")

```
cd <Ruta al laboratorio>/apichol/exercises/ex2
```

### Sumario del ejercicio

En este ejericio haremos.:

1. Aprender acerda de la especificación de OpenAPI 3.0 (Conocida mayormente como Swagger) y sus componentes
2. Aprender a usar el editor de Swagger para diseñar y modificar especificaciones JSON de un API
3. Aprender a importar una especificación OpenAPI (Swagger) en API Designer para posteriores ediciones

### Paso 1: Introducción a OpenAPI y sus componentes

#### [OpenAPI](https://github.com/OAI/OpenAPI-Specification) (Versión actual: 3.0.1)
La especificación de OpenAPI (Conocida anteriormente como Swagger) es el estándar de la industria para definir APIs REST. El objetivo de esta especificación es que sea estándar e independiente de lenguajes de programación para permitir, tanto a humanos como a computadoras, descubrir y entender las capacidades del servicio sin necesidad de acceder al código fuente, documentación o por inspección del tráfico de red. Un buena implementación, vía OpenAPI, es aquella que un consunidor de servicios puede entender e interacturar con ella con una mínima lógica de implementación.

<blockquote>Las especifiaciones de OpenAPI remueven la labor de adivinar como se invocan los servicios</blockquote>

#### [Componentes de OpenAPI](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.1.md)

- Formato: Los archivos que describen APIs RESTful, de acuerdo a las especificaciones OpenAPI, son representados como **Objetos JSON** bajo los estándares JSON. YAML, siendo un superconjunto de JSON, es usado para representar especificaciones de OpenAPI.
- Beneficios: OpenAPI permite generar librerias cliente para un sin número de *runtimes*, generar servidores *stub*, importar definiciones en herramientas de gestión de APIs y herramientas para validar conformidad de las configuraciones.

#### Paso 2: Manipulemos una especificación OpenAPI

Para efectos de edición de Swaggers, usaremos una herramienta gratuita en el web que nos permitirá dar una mirada a la especificación

```
http://editor.swagger.io
```

En el directorio del ejercicio, importatemos en el editor el archivo ``macreduce.mybluemix.net.yaml``

![swagger](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex2/swaggerspec_import.png)

![swagger](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex2/importfile.png)

El YAML es cargado en el editor. Podemos ver que tenemos un panel en la izquierda donde podemos ver el JSON y en la derecha la representación del Swagger.

![swagger](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex2/macreduce.png)

Haremos una modificación para agregar una respuesta a nuestra API. Busquemos, en el JSON, el siguiente texto.

```
  '/mac/{macId}':
      get:
        summary: Retrieves a Mac document
        responses:
          '200':
            description: Mac document fetched successfully
        parameters:
          - in: path
            name: macId
  [...]
```
Agregaremos una respuesta HTTP/404 - Documento no encontrado 

```
  '/mac/{macId}':
      get:
        summary: Retrieves a Mac document
        responses:
          '200':
            description: Mac document fetched successfully
          '404':
            description: Mac document not found
        parameters:
          - in: path
            name: macId
 [...]
```

Explorando el JSON en el editor, podrás ver que se especifican una variedad de elementos. Si se quiere, podemos resumirlos en:
- Tipos de método (get, post, delete, ...)
- Respuestas (200, 400, 404, ...)
- Parámetros
- Rutas
-*content-types* (application/json, application/xml, ...)

Ahora bien, descarguemos nuestro swagger modificado.

![swagger](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex2/downloadjson.png)

El swagger editor es una buena herramienta para modificar especificaciones OpenAPI y, también, para crear especificaciones desde cero.

#### Paso3: ?????

To open the API Designer, on the command line enter:

```
SKIP_LOGIN=true apic edit
```

This should result in the API Designer opening within your default web browser.

Our next step is to import the OpenAPI specification into API Designer.  To accomplish this, click on the **+ Add** link and select the Import OpenAPI choice
<br/><br/>
![importopenapi](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex2/importopenapi.png)

You will want to browse to the location where you downloaded the swagger.json file created from Swagger editor and click on the **Import** button.

This should cause focus on the API Design tab with various fields populated via data found within the OpenAPI specification file.  Feel free to explore the various section links on the left to get a feel for design options available to you.
<br/><br/>
![apidesignview](https://raw.githubusercontent.com/ragsns/apichol/master/images/ex2/apidesignview.png)

It is also worth noting that if you already possess an existing backend API application, you can publish this Open API (Swagger) specification to Bluemix whereby the platform would then manage your existing APIs for you.  Platforms such as Bluemix are great at providing analytics, gateway, security, authentication and user management facilities for your API needs.

### Summary of exercise and next steps
We've now learned quite a bit.  We know what an Open API (Swagger) specification is, how its used and what is its composition.  We've explored a couple of tools that assist us with Open API design, composition and management.

In [Exercise 3](../ex3), we'll create a Loopback Application against these defined APIs.  Having a backend application takes the conceptual descriptions within the spec and makes them concrete (e.g. Functional Create, Read, Update and Delete API endpoints).
