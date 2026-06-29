# LibreNMS2Kafka2Prometheus

This project is to describe how to transport data exported by [LibreNMS](https://librenms.org) into [Prometheus](https://prometheus.io) through a [Kafka](https://kafka.apache.org/) Broker.

To achieve this, we use the data pipeline software, [Vector](https://vector.dev).

## Disclaimer

This is for now a Proof Of Concept (no resiliency is provied as of Now).

## Schema

```mermaid
graph LR;
    LibreNMS --> Kafka;
    Kafka --> Vector;
    Vector --> Prometheus;
```

## Basic LibreNMS configuration for Kafka

This is a basic configuration of LibreNMS to export Data into kafka topic
```
{
    "enable": true,
    "debug": false,
    "security": {
        "debug": ""
    },
    "broker": {
        "list": "<YOUR BROKER HERE>"
    },
    "idempotence": false,
    "topic": "<YOUR TOPIC HERE>",
    "ssl": {
        "enable": false,
        "protocol": null,
        "ca": {
            "location": ""
        },
        "certificate": {
            "location": ""
        },
        "key": {
            "location": "",
            "password": ""
        },
        "keystore": {
            "location": "",
            "password": ""
        }
    },
    "flush": {
        "timeout": 1
    },
    "buffer": {
        "max": {
            "message": 100
        }
    },
    "batch": {
        "max": {
            "message": 10
        }
    },
    "linger": {
        "ms": 100
    },
    "request": {
        "required": {
            "acks": "0"
        }
    }
}
```