# Clase 03 - Poner a Correr ElasticSearch

## Paso 1 - Crear archivo de configuración
- **`mkdir curso-elastic-platzi`**
- **`cd curso-elastic-platzi`**
- Abrir archivo con Sublime (u otro editor de texto)

```python
version: '2.2'
services:
  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.6.0
    container_name: es01
    environment:
      - node.name=es01
      - cluster.name=es-docker-cluster
      - cluster.initial_master_nodes=es01
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data01:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
    networks:
      - elastic

volumes:
  data01:
    driver: local

networks:
  elastic:
    driver: bridge
```

## Paso 2 - Levantar el servicio
- **`docker-compose up`**
- Esperamos a que levante, mientras tanto abrimos **Postman**

```java
GET http://localhost:9200
```
