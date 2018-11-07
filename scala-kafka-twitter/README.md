
### Prueba de concepto big data con data streamming usando Scala, Kafka, Avro y Spark Streaming con Twitter como fuente de streaming

#### ¿Cómo correrlo? (linux)

1. Instalar Java y configurar la variable de entorno

```
$ sudo yum install java-1.8.0-openjdk
```
Editar /etc/environment en cualquier editor como nano or gedit y agrega la siguiente línea:
```
JAVA_HOME=/usr/lib/jvm/open-jdk
```
(el java path igual al de la instalación ejemplo /lib/jvm/java-1.8.0-openjdk)

Usa e comando source para cargar en la terminal actual la variable configurada:
```
source /etc/environment
```
2. Instala e inicia Kafka, puedes seguir las instrucciones pasos 1 a 5 de : https://goo.gl/dkvWH8

3. Inicia el Kafka producer ejecuntado desde esta carpeta:
```
./gradlew produce 
```
Esto iniciará la lectura de los twetts recientes que cumplen con el filtro de los hashtags o palabras configuradas en el archivo Producer de scala y los llevará al tópico de Kafka en formato binario usando Avro

4. Inicia el Kafka consumer ejecutando desde esta carpeta:
```
 ./gradlew consume
```
Esto hará que Spark inicie conectándose al tópico de Kafka, decodificando con Avro los mensajes recuperados y mostrará posteriormente las 10 palabras más populares luego del análisis (conteo de palabras usando mapreduce) cada 5 segundos
 

