# Clase 04 - Índices y Documentos

## Creamos nuestro primer modelo: Usuarios
- Agregaremos un nuevo documento con el id 1 en el **índice usuarios**

```javascript
PUT /usuarios/_doc/1
{
  "nombre": "Rick Sanchez"
}
```

- Result: **Created**
- **_doc** es la uri para acceder y manipular documentos
- Ahora vamos a ejecutar la consulta nuevamente separando nombre y apellido

```java
PUT /usuarios/_doc/1
{
  "nombre": "Rick",
  "apellido": "Sanchez"
}
```

- Result: **Updated**
- Ahora, consultemos el documento creado.

```java
GET /usuarios/_doc/1
```

- Found: **True**

## Creamos otro usuario con POST
- Ahora usemos **POST** para crear otro usuario

```java
POST /usuarios/_doc
{
  "nombre": "Morty",
  "apellido": "Smith"
}
```

- ID **autogenerado**
- Con **POST** no tenemos que indicar ID mientras que con **PUT** si

## A tener en cuenta
- No hemos creado un índice de manera explícita
- ElasticSearch **por defecto** crea uno si no existe
- **Infiere** el tipo de dato de los campos que vayamos agregando
- Podemos **agregar u omitir** campos al crear un documento

## Miremos como crear varios usuarios al tiempo
- Vamos a crear el archivo **usuarios.json** con el siguiente contenido

```java
{ "index" : { "_id" : "3" } }
{ "nombre" : "Beth", "apellido": "Smith" }
{ "index" : { "_id" : "4" } }
{ "nombre" : "Jerry", "apellido": "Smith" }
```

- En Postman, vamos a seleccionar **binary**
- Luego seleccionamos **usuarios.json**
- Luego enviamos la consulta a **`_bulk`**

```java
POST /usuarios/_bulk
```

- **Errors**: False
- **Items**: Lista de resultados para cada uno de los documentos
- Result: **Created** (para todos)
