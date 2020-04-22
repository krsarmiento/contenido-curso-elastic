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

- Al ejecutar un guardado **en código** y de una consultar el documento, **este no se verá**
- `?refresh` sirve para tener cambios enseguida (sin esperar 1 seg)
- No es recomendado por **performance**

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

## Siguiente Clase: Verbos HTTP
