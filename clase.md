# Clase 07 - Puntaje

## Agreguemos un nuevo plato

```java
PUT /platos/_doc/3
{
  "nombre": "Nachos XL",
  "descripcion": "Nachos con carne, guacamole, pico de gallo, salsa picante, queso y frijoles",
  "estado": "activo",
  "pedidosUltimaHora": 11,
  "ultimaModificacion": {
    "usuario": "jsmith@mail.com",
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

- **max_score**: 3.2200139

### **Nachos XL**: 3.2200139 
- palabra **nachos** en **nombre**
- palabras **nachos/queso** en **descripción**
- Mayor coincidencia

### **Ensaladísima**: 0.4471386
- Palabra queso en **descripción**
- Menor coincidencia

## Búsqueda No. 2: Bowl Pollo Saludable

```java
GET /platos/_search
{
  "query": {
    "simple_query_string" : { "query": "bowl pollo saludable" }
  }
}
```

### **Bowl Picante**: 1.9992181
- Bowl en **nombre**
- Pollo en **descripción**

###  **Ensaladísima**: 0.9331132
- Saludable en **descripción**

## Búsqueda No. 3: Guacamole Picante

- Modifiquemos el puntaje agregando **fields**
- Con  **^** modificamos el peso de un campo

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
