# Clase 07 - Puntaje (BE A BIT FAST)

## Agreguemos un nuevo plato

```java
PUT /platos/_doc/3
{
  "nombre": "Nachos XL",
  "descripcion": "Nachos con carne, guacamole, pico de gallo, salsa picante y queso",
  "estado": "activo",
  "pedidosUltimaHora": 11,
  "ultimaModificacion": {
    "usuario": "jerry@mail.com",
    "fecha": "2020-03-01"
  }
}
```

## Búsqueda No. 1: Nachos con queso

- Vamos a realizar una búsqueda simple: **nachos con queso**
- Para búsquedas simples usamos **simple_query_string**

```java
GET /platos/_search
{
  "query": {
    "simple_query_string" : { "query": "nachos con queso" }
  }
}
```

## Búsqueda No. 2: Bowl Pollo Saludable

```java
GET /platos/_search
{
  "query": {
    "simple_query_string" : { "query": "bowl pollo saludable" }
  }
}
```

## Búsqueda No. 3: Guacamole Picante

- Vas a modificar el puntaje agregando **fields**
- Con  **^** modificas el peso de un campo

```java
GET /platos/_search
{
  "query": {
    "simple_query_string" : {
        "query": "guacamole picante",
        "fields": ["nombre^2", "descripcion"]
    }
  }
}
```

### Si **`nombre^2`**
1. Bowl Picante (Palabra picante en título)
2. Nachos XL

### Si **`descripcion^2`**
1. Nachos XL (guacamole y picante en descripción)
2. Bowl Picante

## Siguiente Clase: Tipos de Cláusulas
