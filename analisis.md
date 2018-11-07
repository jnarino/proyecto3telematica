# Informe Proyecto 3

## Problema a resolver

La aplicación realiza un word count de textos emitidos sobre una temática (hashtag o palabra) en tiempo real de la aplicación twitter, la intención es conocer la popularidad de las diferentes palabras en lapsos de 5 segundos

## Arquitectura de datos (ciclo de vida, almacenamiento, procesamiento)

Diseño arquitectura aplicación: https://goo.gl/vMbwWk

Los datos son recuperados y serializados para una mayor eficiencia por el algoritmo en cuestión

## Fuentes y naturaleza de los datos + tecnologías a utilizar

Los tweets son el elemento básico de todo lo que conforma Twitter. Los tweets también se conocen como "actualizaciones de estado". El objeto Tweet tiene una larga lista de atributos de "root-level", incluyendo atributos fundamentales como id, created_at y text. Los objetos de tweet también son el objeto "padre" de varios objetos hijos. Los objetos secundarios de Tweet incluyen usuario, entidades y entidades extendidas. Los tweets que están etiquetados geográficamente tendrán un objeto secundario de lugar ".

El JSON de twitter tiene los siguiente atributos y los elementos hijos estan dados por { }
```javascript
{
 "created_at":"Thu Apr 06 15:24:15 +0000 2017",
 "id": 850006245121695744,
 "id_str": "850006245121695744",
 "text": "1/ Today we’re sharing our vision for the future of the Twitter API platform!nhttps://t.co/XweGngmxlP",
 "user": {},  
 "entities": {}
}
```
## Sistema de ingesta de datos + tecnologías a utilizar

Programa que sirve como controlador entre los datos emitidos en twitter y el pipeline de datos de kafka que será un productor-consumidor de contenidos.

El productor pública la información en tópico elegido. El productor es responsable de elegir qué registro se asigna a que partición dentro del tópico.

El consumidor recupera cada registro publicado bajo un tópico suscrito y se entregan a una instancia del consumidor.

Los datos obtenidos de twitter mediante una aplicación en el lenguaje scala, son serializados con la ayuda del framework Avro y puestos en una cola/tópico de Apache Kafka

## Almacenamiento de los datos + tecnologías a utilizar

Kafka persiste la información en disco la cual se define en una política de almacenamiento de datos dentro de un log por un tiempo definido.  La información se sigue publicando esté o no siendo consumida.

## Análisis de datos + tecnologías a utilizar

En el consumer usa spark al cual se le asigna a un tópico y hace un streaming de la info en memoria decodificando con Avro para luego hacer una implementación de un wordcount con mapreduce.

El resultado es mostrado en consola cada 5 segundos.
