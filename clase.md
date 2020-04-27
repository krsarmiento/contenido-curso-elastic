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
        "gt": 3.5,
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
        "gte": "2020-01-15",
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

### Indicamos que para los restaurantes sin calificación, por defecto es **3.0** (SUBWAY)

- 

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

## Próxima clase: Revisión Final Del Directorio
