# API Connect Hands-On Lab

## Prerrequisitos

Además de necesitar una computadora, necesitarás el siguiente software antes de empezar el laboratorio:
-	Git: http://git-scm.com/downloads
- CLI de Cloud Foundry: https://github.com/cloudfoundry/cli#downloads
- npm para NodeJs: https://nodejs.org/en/download/
- API Connect Developer Kit: https://www.npmjs.com/package/apiconnect

También precisarás una cuenta en IBM Cloud: https://console.bluemix.net/registration/

Las versiones que se precisan deben ser mayor o igual a las presentadas a continuación:

```
git --version
git version 2.15.0
```

```
cf --version
cf version 6.37.0+XXXXXXXXX
```

```
node --version
v8.9.1
```

```
npm --version
6.1.0
```

```
apic --version
API Connect: v5.0.8.3
```

## Recursos para el Lab

Los ejercicios y una presentación está disponible en https://github.com/surasiterix/apichol. Clona el repositorio en tu máquina para tener el material del curso.

```
git clone https://github.com/surasiterix/apichol
```

## Inmportante recordar

Cada ejercicio tiene un subdirectorio. ***Asegúrate de estar en el subdirectorio acorde con el número de ejercicio, sobre todo al ejecutar comandos desde la CLI***

## Ejercicios disponibles en este Lab

Los ejercicios están pensados para realizarse secuencialmente, ya que son progresivos y dependientes entre si. Cada ejercicio está pensado para desarrollarse entre 5 y 10 minutos.

- Ejercicio 1: [Instalar Node.js y el toolkit de API Connect](exercises/ex1)
- Ejercicio 2: [Diseñar especificaciones swagger OpenAPI](exercises/ex2)
- Ejercicio 3: [Generar aplicaciones LoopBack e importar APIs](exercises/ex3)
- Ejercicio 4: [Crear un servicio de base de datos en IBM Cloud](exercises/ex4)
- Ejercicio 5: [Crear APIs CRUD a base de datos con modelos LoopBack](exercises/ex5)
- Ejercicio 6: [Probar, Explorar y desplegar aplicaciones LoopBack](exercises/ex6)
- Ejercicio 7: [Explorar APIs desplegados con API Manager en IBM Cloud](exercises/ex7)
- Ejercicio 8: [Tour A - Crear una API metereológica usando API Connect en IBM Cloud](exercises/ex8)
- Ejercicio 9: [Tour B - Generar un Portal de desarrolladores para tus APIs metereológicas](exercises/ex9)

## Mas información

Tutoriales de API Connect en https://console.ng.bluemix.net/docs/services/apiconnect/index.html

Manual de referencia (Knowledge Center) del Developer Toolkit de API Connect en https://www.ibm.com/support/knowledgecenter/SSMNED_5.0.0/mapfiles/getting_started.html

Documentación para LoopBack en http://loopback.io/

## Agradecimientos

Este laboratorio fue adaptado del original (https://github.com/ibm-apiconnect/apichol) para el IBM Code Day en Montevideo (http://ibmcodedaymvd.com)

Síguenos en twitter @IBMUruguay
