# Clase 14 - Consultas de Rango y Agregaciones

## Consultas de rango

### Búsqueda No. 1 - 3.5 <= calificacion <= 4.5
- Usamos **`_source`** para indicar que campos queremos obtener

```java
GET /restaurantes/_search
{
  "_source": ["nombre", "calificacion"],
  "query": {
    "range": {
      "calificacion": {
        "gte": 3.5,
        "lte": 4.5
      }
    }
  }
}
```

### Búsqueda No. 2 - Ultima modificación desde la segunda mitad de Enero hasta finales de Febrero

```java
GET /restaurantes/_search
{
  "_source": ["nombre", "ultimaModificacion.fecha"],
  "query": {
    "range": {
      "ultimaModificacion.fecha": {
        "gte": "2020-02-15",
        "lt": "2020-03-01"
      }
    }
  }
}
```

## Agregaciones

### Obtenemos métricas de los restaurantes actuales

```java
GET /restaurantes/_search
{
    "aggs" : {
        "calificacionPromedio": { "avg" : { "field" : "calificacion" } },
        "calificacionMaxima": { "max" : { "field" : "calificacion" } },
        "calificacionMinima": { "min" : { "field" : "calificacion" } }
    }
}
```

- min: 3.17
- max: 4.22
- promedio: 3.713

### Creamos nuevo restaurante sin datos

```java
PUT /restaurantes/_doc/4
{
    "nombre": "Los Pollos Hermanos",
    "ultimaModificacion": {
        "fecha": "2020-03-15",
        "nombreCompleto": "Gustavo Fring",
        "email": "gustavo@vendor.com"
    }
}
```

- Indicamos que para los restaurantes sin calificación, por defecto es **3.0**

```java
GET /restaurantes/_search
{
    "aggs" : {
        "calificacionPromedio" : {
            "avg" : {
                "field" : "calificacion",
                "missing": 3.0
            } 
        }
    }
}
```

- Promedio cambia porque hay un nuevo valor
- promedio: 3.535

## Próxima clase: Consultas de Rango y Agregaciones
