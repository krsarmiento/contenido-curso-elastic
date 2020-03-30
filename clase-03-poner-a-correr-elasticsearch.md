# Clase 03 - Poner a Correr ElasticSearch

- Para correr el servicio de ElasticSearch en nuestros ambientes locales vamos a utilizar Docker.
- **`mkdir curso-elastic-platzi`**
- **`cd curso-elastic-platzi`**
- **`nano docker-compose.yml`** (editor de texto)

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

- **`ls`**
- Este archivo describe a docker como va a **levantar** el servicio de ElasticSearch
- Nos basamos en la **documentación oficial**, el link queda como enlace.
- Servicio llamado **es01**
- Versión **7.6.0**
- ElasticSearch corre por defecto en el puerto **9200**
- **`docker-compose up`**
- Esperamos a que el servicio termine de levantar, mientras tanto abrimos **Postman**
- Postman: **GET http://localhost:9200**
- En el resultado podemos ver el nombre del servicio y la versión que especificamos
- ElasticSearch ya está listo para recibir datos.
