# Clase 04 - Índices y Documentos

## Creamos nuestro primer modelo: Usuarios

```javascript
PUT /usuarios/_doc/1
{
  "nombre": "Rick",
  "apellido": "Sanchez"
}
```

## Creamos otro usuario con POST

```java
POST /usuarios/_doc?refresh
{
  "nombre": "Morty Smith"
}
```

- ID **autogenerado**
- Con **POST** no tenemos que indicar ID mientras que con **PUT** si

- `?refresh` sirve para tener cambios enseguida (sin esperar 1 seg)
- No es recomendado por **rendimiento**

## A tener en cuenta
- No creaste un índice de manera explícita
- ElasticSearch **por defecto** crea uno si no existe
- Puedes **agregar u omitir** campos al crear un documento

## Miremos como crear varios usuarios al tiempo
- Vas a crear el archivo **usuarios.json** con el siguiente contenido

```java
{ "index" : { "_id" : "3" } }
{ "nombre" : "Beth", "apellido": "Smith" }
{ "index" : { "_id" : "4" } }
{ "nombre" : "Jerry", "apellido": "Smith" }
```

- En Postman, seleccionas **binary**
- Luego seleccionas el archivo **usuarios.json**
- Luego envias un **POST** a **`_bulk`**

```java
POST /usuarios/_bulk
```

## Siguiente Clase: Verbos HTTP
