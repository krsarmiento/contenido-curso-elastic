# Clase 09 - Clausulas Booleanas

- Retorna documentos que coincidan con las combinaciones de ocurrencias dentro de ella
- [Índice de Platos] Vamos a hacer un a consulta booleana con todas las cláusulas

```java
GET /platos/_search
{
  "query": {
    "bool" : {
      "must" : {
        "match" : { "descripcion" : "picante" }
      },
      "filter": {
        "term" : { "estado" : "activo" }
      },
      "must_not" : {
        "term" : { "pedidosUltimaHora" : 0 }
      },
      "should" : [
        { "match" : { "descripcion" : "aguacate" } },
        { "match" : { "descripcion" : "guacamole" } }
      ]
    }
  }
}
```

- Dos resultados (1.3802519, 1.0470967)
- Ni estado=activo ni pedidosUltimaHora=0 contribuyen al puntaje
- must, filter y must_not contienen una sola consulta (usamos {}) 
- should contiene varias consultas (usamos [])
- Movemos estado=activo a must para que afecte el puntaje (ahora must debe ser [])


```java
GET /platos/_search
{
  "query": {
    "bool" : {
      "must" : [
        { "match" : { "descripcion" : "picante" } },
        { "term" : { "estado" : "activo" } }
      ],
      "must_not" : {
        "term" : { "pedidosUltimaHora" : 0 }
      },
      "should" : [
        { "match" : { "descripcion" : "aguacate" } },
        { "match" : { "descripcion" : "guacamole" } }
      ]
    }
  }
}
```

- Mismos dos resultados (1.5137832, 1.1806281)
- El puntaje subió para ambos porque tienen estado=activo
- De las dos consultas en should, solo una debe hacer match (minimum_should_match=1 por defecto)
- Ahora minimum_should_match=2
- Agreguemos otra consulta a should (descripcion=frijoles)

```java
GET /platos/_search
{
  "query": {
    "bool" : {
      "must" : [
        {"match" : { "descripcion" : "picante" } },
        {"term" : { "estado" : "activo" } }
      ],
      "must_not" : {
        "term" : { "pedidosUltimaHora" : 0 }
      },
      "should" : [
        { "match" : { "descripcion" : "aguacate" } },
        { "match" : { "descripcion" : "guacamole" } },
        { "match" : { "descripcion" : "pico de gallo" } }
      ],
      "minimum_should_match": 2
    }
  }
}
```

- Nachos XL: guacamole y pico de gallo en descripción
