# JAVA 

## Objetivo

Asimilar los conceptos mediante el uso del lenguaje java ☕️

## Build

Para construir el proyecto usaremos **maven**. 

Podemos usar nuestro IDE de referencia o la línea de comando.

```bash
mvn clean install
```

## Simple Client

### Producer API

Las clases relativas a la producción son **Producer** y **ProducerApp**

Del mismo modo, para ejecutar la aplicación productora podemos usar nuestro IDE o la linea de comandos

```bash
mvn dependency:copy-dependencies
```

```bash
java -cp  "target/classes:target/dependency/*" com.ucmmaster.kafka.simple.ProducerApp    
```

Deberías empezar a ver logs en la pantalla

### Consumer API

Las clases relativas a la producción son **Consumer** y **ConsumerApp**

En este caso abre una nueva terminal para poder tener ejecutando a la vez productor y consumidor

```bash
java -cp  "target/classes:target/dependency/*" com.ucmmaster.kafka.simple.ConsumerApp    
``` 

Deberías empezar a ver logs en la pantalla

ConsumerApp crea una aplicación consumidora con 2 consumers.

Fíjate en los logs, que los threads **[Thread-0]** y **[Thread-1]** están consumiendo topics de sus respectivas particiones

Si ejecutas la aplicación consumidora desde el IDE, es posible matar unos de estos threads, y por lo tanto podremos ver el rebalanceo de las particiones de ese consumidor al otro

> ❗️ **NOTA**<br/>Para detener una aplicación de consola debemos pulsar **Ctrl+C**
 
> 📚 **NOTA**<br/>La configuración tanto del productor como del consumidor están externalizadas en el fichero **simple-client.properties**

> 💊 **NOTA**<br/>Lee el código de todas las clases<br/>Analiza las clases de [Producer](https://kafka.apache.org/39/javadoc/index.html?org/apache/kafka/clients/producer/KafkaProducer.html) y [Consumer](https://kafka.apache.org/39/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html) API <br/> Trata de hacer pequeñas modificaciones

## Avro Client

En este ejemplo, vamos a hacer lo mismo pero esta vez haciendo uso de un **data contract** expresado con un esquema AVRO.

### Data Contract

El contrato de datos se encuentra definido en com.ucmmaster.kafka.avro.TemperatureRead.avsc

La generación de la correspondiente clase TemperatureRead.java se hace a través de un plugin maven.

### Producer API

Las clases relativas a la producción son **Producer** y **ProducerAvroApp** dentro del paquete com.ucmmaster.kafka.avro

Del mismo modo, para ejecutar la aplicación productora podemos usar nuestro IDE o la linea de comandos

```bash
mvn dependency:copy-dependencies
```

```bash
java -cp  "target/classes:target/dependency/*" com.ucmmaster.kafka.avro.ProducerAvroApp    
```

Deberías empezar a ver logs en la pantalla

### Consumer API

Las clases relativas a la producción son **Consumer** y **ConsumerAvroApp** dentro del paquete com.ucmmaster.kafka.avro

En este caso abre una nueva terminal para poder tener ejecutando a la vez productor y consumidor

```bash
java -cp  "target/classes:target/dependency/*" com.ucmmaster.kafka.avro.ConsumerAvroApp    
``` 

### Control Center

Explora a través de [Control Center](http://localhost:9021/clusters/Nk018hRAQFytWskYqtQduw/management/topics/temperature-telemetry-avro/settings) los mensajes y el esquema registrado

### Schema Registry

Explora los siguientes endpoints del Schema Registry:

http://localhost:8081/schemas

http://localhost:8081/subjects

http://localhost:8081/subjects/temperature-telemetry-avro-value/versions

http://localhost:8081/subjects/temperature-telemetry-avro-value/versions/1

### Console Consumer

Vamos a probar a consumir los mensajes desde la herramienta de consola:

¿Qué pasará?

```bash
kafka-console-consumer --bootstrap-server broker-1:29092 --topic temperature-telemetry --property print.key=true    
``` 

> ❗️ **NOTA**<br/>Para detener una aplicación de consola debemos pulsar **Ctrl+C**

> 📚 **NOTA**<br/>La configuración tanto del productor como del consumidor están externalizadas en el fichero **avro-client.properties**

> 🔎 Presta especial atención a las clases de los **serdes** en el fichero properties, son clases del librerias de Confluent

> 💊 **NOTA**<br/>Lee el código de todas las clases<br/>Analiza las clases de [Producer](https://kafka.apache.org/39/javadoc/index.html?org/apache/kafka/clients/producer/KafkaProducer.html) y [Consumer](https://kafka.apache.org/39/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html) API <br/> Trata de hacer pequeñas modificaciones