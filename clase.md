# Clase 11 - Construyendo una consulta compuesta

```java
GET /platos/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "bool": {
            "should": [
              { "term": { "estado": "activo"} },
              { "term": { "estado": "agotado"} }
            ]
          }
        },
        {
          "bool": {
            "should": [
              {
                "match": {
                  "ultimaModificacion.usuario": "mail.com"
                }
              },
              {
                "match": {
                  "ultimaModificacion.usuario": "vendor.com"
                }
              }
            ]
          }
        },
        {
          "term": { "pedidosUltimaHora": 0 }
        }
      ]
    }
  }
}
```

- Ensaladísima: **activo**, rsanchez@**mail.com**, **cero pedidos**

## Próxima clase: Consultas Anidadas
