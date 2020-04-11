# Clase 13 - Proyecto: Unificación de Datos

## Paso 1 - Consultamos el mapeo actual de los índices

```java
GET /restaurantes/_mapping
```

```java
GET /platos/_mapping
```

## Paso 2 - Actualizamos restaurantes con platos y nuevos campos

```java
PUT /restaurantes/_mapping
{
  "properties":{
    "calificacion": { "type": "double" },
    "direccion": { "type": "text" },
    "telefono": { "type": "keyword" },
    "platos": {
      "type": "nested",
      "properties": {
        "descripcion": { "type": "text" },
        "estado": { "type": "keyword" },
        "nombre": { "type": "text" },
        "pedidosUltimaHora": { "type": "integer" }
      }
    },
    "ultimaModificacion": {
      "properties": {
        "nombreCompleto": { "type": "text" },
        "email": { "type": "text" },
        "fecha": { "type": "date" }
      }
    }
  }
}
```

## Paso 3 - Actualizamos restaurantes existentes con **POST y `_update`**

```java
POST /restaurantes/_update/1
{
  "doc": {
    "calificacion": 4.22,
    "direccion": "Calle Primera, Barrio Centro",
    "telefono": "111232323",
    "platos": [
      {
        "nombre": "Bowl Picante",
        "descripcion": "Pollo, salsa picante, frijoles negros, plátano maduro y aguacate.",
        "estado": "activo",
        "pedidosUltimaHora": 42
      }
    ],
    "ultimaModificacion": {
      "nombreCompleto": "Rick Sanchez",
      "email": "rsanchez@mail.com",
      "fecha": "2020-03-04"
    }
  }
}
```

```java
POST /restaurantes/_update/2
{
  "doc": {
    "calificacion": 3.75,
    "direccion": "Carrera Segunda, Barrio Occidental",
    "telefono": "444565656",
    "platos": [
      {
        "nombre": "Nachos XL",
        "descripcion": "Nachos con carne moplida, guacamole, pico de gallo, salsa picante, queso chedar y frijoles negros",
        "estado": "activo",
        "pedidosUltimaHora": 11
      }
    ],
    "ultimaModificacion": {
      "nombreCompleto": "Morty Smith",
      "email": "msmith@mail.com",
      "fecha": "2020-02-26"
    }
  }
}
```

```java
POST /restaurantes/_update/3
{
  "doc": {
    "calificacion": 3.17,
    "direccion": "Carrera Tercera, Barrio Norte",
    "telefono": "777898989",
    "platos": [
      {
        "nombre": "Ensaladísima",
        "descripcion": "Aceitunas, cebolla, queso, pimentón, tomate cherry, aguacate. (vegetariano y saludable)",
        "estado": "activo",
        "pedidosUltimaHora": 0
      }
    ],
    "ultimaModificacion": {
      "nombreCompleto": "Summer Smith",
      "email": "ssmith@mail.com",
      "fecha": "2020-02-17"
    }
  }
}
```

## Paso 4 - Vemos como quedó nuestro directorio de restaurantes

```java
GET /restaurantes/_search
```
