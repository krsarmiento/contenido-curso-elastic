# Clase 12 - Consultas Anidadas

- Crear índice restaurantes con nombre, categorias (una de ellas principal)

```java
PUT /restaurantes
{
  "mappings":{
    "properties":{
      "nombre":{
        "type":"text"
      },
      "categorias" : {
        "type" : "nested",
        "properties": {
          "nombre": { "type" : "term" },
          "principal": { "type" : "boolean" }
        }
      }
    }
  }
}
```

- categorias de tipo nested
- Agreguemos restaurantes

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

- Buscamos restaurantes con categoria **Comida Rápida**
- Usamos consulta **nested**

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
            }
          ]
        }
      }
    }
  }
}
```

- Dos resultados
- Se retorna el documento completo en ambos
- Buscamos **Comida Rápida** como categoría principal


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

- McDonald's solamente
- Buscamos otra categoría como principal: **Comida Saludable**

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

- Cero Resultados
