# kafka
Comandos útiles para Kafka

Si Kafka corre a través de Docker ejecutar este comando para entrar dentro del contenedor:

```
docker exec -it <CONTAINER_NAME> bash
```

## Gestión de brokers

| Comando                                                                                                          | Uso                                                     |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| `kafka-topics.sh --list --bootstrap-server <BROKER>`                                                             | Lista todos los topics del cluster                      |
| `kafka-topics.sh --create --topic <TOPIC> --bootstrap-server <BROKER> --partitions <N> --replication-factor <N>` | Crear un topic con particiones y factor de replicación  |
| `kafka-topics.sh --describe --topic <TOPIC> --bootstrap-server <BROKER>`                                         | Ver información de un topic (particiones, líderes, ISR) |
| `kafka-topics.sh --delete --topic <TOPIC> --bootstrap-server <BROKER>`                                           | Borrar un topic                                         |
| `kafka-broker-api-versions.sh --bootstrap-server <BROKER>`                                                       | Ver versión y APIs soportadas por el broker             |

## Producción y consumo de mensajes

| Comando                                                                                                                        | Uso                                              |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------ |
| `kafka-console-producer.sh --topic <TOPIC> --bootstrap-server <BROKER>`                                                        | Enviar mensajes manualmente al topic             |
| `kafka-console-consumer.sh --topic <TOPIC> --bootstrap-server <BROKER> --from-beginning`                                       | Leer mensajes desde el principio                 |
| `kafka-console-consumer.sh --topic <TOPIC> --bootstrap-server <BROKER> --group <GROUP>`                                        | Leer mensajes desde un consumer group específico |
| `kafka-consumer-groups.sh --bootstrap-server <BROKER> --describe --group <GROUP>`                                              | Ver offsets y lag de un consumer group           |
| `kafka-consumer-groups.sh --bootstrap-server <BROKER> --reset-offsets --to-earliest --execute --topic <TOPIC> --group <GROUP>` | Resetear offsets a inicio (útil para testing)    |

## Administración de topics avanzada

| Comando                                                                                                                           | Uso                                               |
| --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| `kafka-topics.sh --alter --topic <TOPIC> --partitions <N> --bootstrap-server <BROKER>`                                            | Aumentar número de particiones de un topic        |
| `kafka-configs.sh --bootstrap-server <BROKER> --entity-type topics --entity-name <TOPIC> --describe`                              | Ver configuración de un topic                     |
| `kafka-configs.sh --bootstrap-server <BROKER> --entity-type topics --entity-name <TOPIC> --alter --add-config retention.ms=60000` | Cambiar configuración de un topic (ej: retención) |
| `kafka-reassign-partitions.sh --bootstrap-server <BROKER> --reassignment-json-file <FILE> --execute`                              | Rebalancear particiones entre brokers             |

## Diagnóstico y monitorización

| Comando                                                                                                | Uso                                         |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------- |
| `kafka-topics.sh --describe --topic <TOPIC>`                                                           | Ver líder de cada partición, replicas y ISR |
| `kafka-run-class.sh kafka.tools.JmxTool`                                                               | Conectar JMX para métricas del broker       |
| `kafka-log-dirs.sh --bootstrap-server <BROKER> --describe`                                             | Ver tamaño de logs y particiones por broker |
| `kafka-consumer-groups.sh --bootstrap-server <BROKER> --list`                                          | Listar todos los consumer groups            |
| `kafka-producer-perf-test.sh --topic <TOPIC> --num-records <N> --record-size <BYTES> --throughput <N>` | Test de performance de productores          |
| `kafka-consumer-perf-test.sh --bootstrap-server <BROKER> --topic <TOPIC> --messages <N>`               | Test de performance de consumidores         |

## Seguridad y autenticación

| Comando                                                                                                                            | Uso                                          |
| ---------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| `kafka-configs.sh --bootstrap-server <BROKER> --entity-type users --alter --add-config SCRAM-SHA-512=password`                     | Configurar usuarios SCRAM para autenticación |
| `kafka-acls.sh --authorizer-properties zookeeper.connect=<ZK> --add --allow-principal User:<USER> --operation All --topic <TOPIC>` | Configurar ACLs para topics                  |
| `kafka-acls.sh --authorizer-properties zookeeper.connect=<ZK> --list`                                                              | Listar todas las ACLs                        |



