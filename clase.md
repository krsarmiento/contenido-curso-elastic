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

- Ensaladísima: **activo**, crd07@**mail.com**, **cero pedidos**
- Ningun plato estado=agotado, pero devuelve resultados por estar en un **OR** con **estado=activo**
