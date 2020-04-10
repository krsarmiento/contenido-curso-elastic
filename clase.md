# Clase 12 - Consultas Anidadas

## Modelo Restaurantes
- Creamos índice con **nombre y categorias** (una de ellas principal)

```java
PUT /restaurantes
{
  "mappings":{
    "properties":{
      "nombre":{ "type":"text" },
      "categorias" : {
        "type" : "nested",
        "properties": {
          "nombre": { "type" : "keyword" },
          "principal": { "type" : "boolean" }
        }
      }
    }
  }
}
```

## Agreguemos restaurantes

```java
PUT /restaurantes/_doc/1
{
  "nombre": "McDonalds",
  "categorias": [
    { "nombre": "Comida Rápida", "principal": true },
    { "nombre": "Desayunos", "principal": false },
    { "nombre": "Hamburguesas", "principal": false }
  ]
}
```

```java
PUT /restaurantes/_doc/2
{
  "nombre": "Burger King",
  "categorias": [
    { "nombre": "Comida Rápida", "principal": false },
    { "nombre": "Hamburguesas", "principal": true }
  ]
}
```

```java
PUT /restaurantes/_doc/3
{
  "nombre": "Subway",
  "categorias": [
    { "nombre": "Comida Saludable", "principal": false },
    { "nombre": "Sándwiches", "principal": true }
  ]
}
```

# Búsqueda No. 1: Categoria=Comida Rápida 

```java
GET /restaurantes/_search
{
  "query": {
    "nested": {
      "path": "categorias",
      "query": {
        "bool": {
          "must": {
            "term": { "categorias.nombre": "Comida Rápida" }
          }
        }
      }
    }
  }
}
```

# Búsqueda No. 2: Categoria=Comida Rápida, principal=true


```java
GET /restaurantes/_search
{
  "query": {
    "nested": {
      "path": "categorias",
      "query": {
        "bool": {
          "must": [
            {
              "term": { "categorias.nombre": "Comida Rápida" }
            },
            {
              "term": { "categorias.principal": true }
            }
          ]
        }
      }
    }
  }
}
```

# Búsqueda No. 3: Categoria=Comida Saludable, principal=true 

```java
GET /restaurantes/_search
{
  "query": {
    "nested": {
      "path": "categorias",
      "query": {
        "bool": {
          "must": [
            {
              "term": { "categorias.nombre": "Comida Saludable" }
            },
            {
              "term": { "categorias.principal": true }
            }
          ]
        }
      }
    }
  }
}
```

# Búsqueda No. 4: Categoria=Comida Saludable

```java
GET /restaurantes/_search
{
  "query": {
    "nested": {
      "path": "categorias",
      "query": {
        "bool": {
          "must": [
            {
              "term": { "categorias.nombre": "Comida Saludable" }
            }
          ]
        }
      }
    }
  }
}
```
