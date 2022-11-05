# meli-proxy

``
Meli Proxy para api.mercadolibre.com
``

## Tech Stack
![image](https://img.shields.io/badge/json-5E5C5C?style=for-the-badge&logo=json&logoColor=white)
![image](https://img.shields.io/badge/OpenJDK-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![image](https://img.shields.io/badge/redis-%23DD0031.svg?&style=for-the-badge&logo=redis&logoColor=white)


## Diagrama de flujo
![Alt text](Meli.drawio.png?raw=true "Title")

## Escalabilidad
### Scale up
Scaleup: Cuando la CPU supere el 80%
Scaledown: Cuando baje el tráfico

### Scale out
Escalar hacía arriba no siempre da abaste, por lo cual se piensa en reautilizar la regionalización de ML.
Con esto se podra realizar un scaleout, agregando mas pods/nodos de nuestro proyecto a la región especifica
pudiendo maantener una carga activa para momentos criticos (Navidad, Comerciales Televisivos, etc)

En general se trabaja con scaleout automatizado, lo que permite no tener que intervenir manualmente el proyecto, con configuraciones
previas, que permite realizar un scaleout o scalein dependiendo de los periodos de prueba.

## Load test
Se realiza una prueba de carga con jmeter para un endpoint get en especifico y este soporta....

## Rate limit
Se define un rate limit por ip (ej 100 peticiones) y por la tupla ip + path (ej: 127.0.0.1 /categories/MLA5725)
Estas son definidas en un archivo yaml (en el futuro pueden ser configuradas en una base de datos)

### Auth rate
Se piensa en un rate limit para solicitantes autorizados a los cuales no queremos bloquear en caso de un DOS.
Estos puede utilizar un app-key y app-id o un jwt. Con esto el proxy permite mantener vivas las solicitudes que son criticas.

## Cache
Se utiliza el cache para bajar la respuesta de 400 ms a un endpoint a 20 ms.

Debemos evaluar cuando vamos a realizar caché.

1) Ya no es válido por tiempo
2) Es una petición repetida
3) No estaba en cache anteriormente

* Hay peticiones que no queremos agregar al cache ya que son distintas cada vez




## Java version
This was used using sdk man https://sdkman.io/install
``
sdk install java 19-amzn
``


## How to run

``
brew install redis 
redis-server
./gradlew bootRun
``