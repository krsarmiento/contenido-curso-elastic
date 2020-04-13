# Clase 15 - Proyecto: Revisión final del directorio

```java
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "calificacion": {
              "gte": 3.5
            }
          }
        },
        {
          "nested": {
            "path": "platos",
            "query": {
              "bool": {
                "must": {
                  "match": {
                    "platos.descripcion": "guacamole picante"
                  }
                }
              }
            }
          }
        }
      ]
    }
  }
}
```

