# Clase 09 - Consultas Booleanas (TAKE IT EASY)

- Retorna documentos que coincidan con las **combinaciones de ocurrencias** dentro de ella

## Consultamos usando todos los tipos de cláusulas

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
      ],
      "minimum_should_match": 1
    }
  }
}
```

- **must** y **filter** acompañan a **should**
- Debemos indicar **minimum_should_match=1**
- Dos resultados (1.3802519, 1.0470967)
- Ni **estado=activo** ni **pedidosUltimaHora=0** contribuyen al puntaje
- **must, filter y must_not** contienen una sola consulta (**usamos {}**) 
- **should** contiene varias consultas (**usamos []**)

## Hacemos que el estado afecte el puntaje
- Movemos **estado=activo** a **must** para que afecte el puntaje 
- ahora must debe ser una lista (**[]**)

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
      ],
      "minimum_should_match": 1
    }
  }
}
```

- Mismos dos resultados (1.5137832, 1.1806281)
- Puntaje **subió** porque **estado** ahora influye al puntaje
- De las dos consultas en **should**, solo una debe hacer match (**minimum_should_match=1**)

## **minimum_should_match=2**
- Agreguemos otra consulta a **should** (**descripcion=pico de gallo**)

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

- **Nachos XL**: **guacamole** y **pico de gallo** en descripción

## Próxima Clase: Consultas Compuestas
