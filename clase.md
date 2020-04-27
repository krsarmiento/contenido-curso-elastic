# Clase 06 - Mapeo de Datos

## Creamos índice con mapeo
- Vamos a crear nuestro segundo modelo: Platos
- Usaremos un **mapeo explícito** para crear el índice

```java
PUT /platos
{
  "mappings":{
    "properties":{
      "nombre":{ "type":"text" },
      "descripcion":{ "type":"text" },
      "pedidosUltimaHora":{ "type":"integer" },
      "ultimaModificacion":{
        "properties": {
          "usuario":  { "type": "text" },
          "fecha":  { "type": "date" }
        }
      }
    }
  }
}
```

- Supongamos que toca agregar un nuevo campo
- podemos actualizar el mapeo con **PUT**

```java
PUT /platos/_mapping
{
  "properties":{
    "estado":{ "type":"keyword" }
  }
}
```

## Creamos platos de ejemplo

```java
PUT /platos/_doc/1
{
  "nombre": "Bowl Picante",
  "descripcion": "Pollo, salsa picante, frijoles, plátano y aguacate",
  "estado": "activo",
  "pedidosUltimaHora": 42,
  "ultimaModificacion": {
    "usuario": "rick@mail.com",
    "fecha": "2020-02-19"
  }
}
```

```java
PUT /platos/_doc/2
{
  "nombre": "Ensaladísima",
  "descripcion": "Aceitunas, cebolla, queso, tomate, aguacate (saludable)",
  "estado": "activo",
  "pedidosUltimaHora": 0,
  "ultimaModificacion": {
    "usuario": "rick@mail.com",
    "fecha": "2020-01-22"
  }
}
```

## Siguiente Clase: Puntaje
