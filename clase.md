# Clase 15 - Proyecto: Revisión final del directorio

## Paso 1 - Vemos todos los datos en nuestro directorio de restaurantes

```java
GET /restaurantes/_search
```

- Contamos con todos los campos necesarios
- Platos y Categorías son objetos anidados de un Restaurante
- Tenemos los datos básicos del restaurante
- Guardamos la información del Usuario que modificó por última vez al restaurante

## Paso 2 - Filtrar el directorio usando datos de Restaurantes y Platos a la vez

- Obtener todos los restaurantes que:
1. Estén ubicados en el **Barrio Centro** o en el **Barrio Occidental**
2. Que sean de **comida rápida** ó que vendan **nachos**

```java
{
  "query": {
    "bool": {
      "must": [
        {
          "bool": {
            "should": [
              {
                "match": {
                  "direccion": "centro"
                }
              },
              {
                "match": {
                  "direccion": "occidental"
                }
              }
            ]
          }
        },
        {
          "bool": {
            "should": [
              {
                "nested": {
                  "path": "categorias",
                  "query": {
                    "bool": {
                      "must": {
                        "term": {
                          "categorias.nombre": "Comida Rápida"
                        }
                      }
                    }
                  }
                }
              },
              {
                "nested": {
                  "path": "platos",
                  "query": {
                    "bool": {
                      "must": {
                        "match": {
                          "platos.descripcion": "nachos"
                        }
                      }
                    }
                  }
                }
              }
            ]
          }
        }
      ]
    }
  }
}
```
