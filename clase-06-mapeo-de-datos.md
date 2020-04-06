# Clase 06 - Mapeo de Datos

- Vamos a crear nuestro segundo modelo: Platos
- Usaremos un **mapeo explícito**

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
- Ahora, vamos a crear los platos que vimos al inicio

```java
POST /platos/_doc/1
{
  "nombre": "Bowl Picante",
  "descripcion": "Pollo, salsa picante, frijoles negros, plátano maduro y aguacate.",
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
  "descripcion": "Aceitunas, cebolla, queso, pimentón, tomate cherry, aguacate. (vegetariano y saludable)",
  "estado": "activo",
  "pedidosUltimaHora": 0,
  "ultimaModificacion": {
    "usuario": "crd07@mail.com",
    "fecha": "2020-01-22"
  }
}
```
