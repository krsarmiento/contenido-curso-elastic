# Clase 06 - Mapeo de Datos

- **Mapeo por defecto** si no lo especificamos
- Para **rendimiento óptimo**: crear mapeo
- Ejemplo: ElasticSearch puede guardar texto como **text** y **keyword**
- **text** es perfecto para búsquedas de texto completo
- **text** falla si queremos buscar el valor exacto, mejor usar **keyword**

## Tipos de datos en ElasticSearch

- **strings**: text, keyword
- **fechas**: date
- **números**: integer, long, float, double
- **booleanos**: boolean
- **objetos**: object, nested
- **geográficos**: geo_point, geo_shape

- Vamos a crear un índice con un **mapeo explícito**

```java
PUT /platos
{
  "mappings":{
    "properties":{
      "nombre":{
        "type":"text"
      },
      "descripcion":{
        "type":"text"
      },
      "pedidosUltimaHora":{
        "type":"integer"
      },
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
    "estado":{
      "type":"keyword"
    }
  }
}
```

- nombre es **text** (búsqueda libre)
- estado **keyword** (búsqueda exacta)
- estados permitidos: **activo, pendiente e inactivo**
- si búscamos **activ** la búsqueda no tendrá resultados
- si fuera **text**, buscar **activ** retornaría **activo, inactivo**
- Por eso es importante diferenciarlos
- Vamos a crear un par de platos de prueba

```java
POST /platos/_doc/1
{
  "nombre": "Bowl Picante",
  "descripcion": "Pollo, salsa picante, frijoles negros, chicharrón, plátano maduro y aguacate.",
  "estado": "activo",
  "pedidosUltimaHora": 42,
  "ultimaModificacion": {
    "usuario": "crd07@mail.com",
    "fecha": "2020-02-19"
  }
}
```

```java
PUT /platos/_doc/2
{
  "nombre": "Ensaladísima",
  "descripcion": "Aceitunas negras, cebolla roja, queso, pimentón amarillo, tomate cherry, aguacate, ajonjolí. (vegano, vegetariano y saludable)",
  "estado": "activo",
  "pedidosUltimaHora": 0,
  "ultimaModificacion": {
    "usuario": "crd07@mail.com",
    "fecha": "2020-01-22"
  }
}
```
