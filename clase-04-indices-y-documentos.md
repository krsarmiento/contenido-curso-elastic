# Clase 04 - Índices y Documentos

- Comencemos creando nuestro primer modelo: Usuarios
- Agregaremos un nuevo documento con el id 1 en el **índice usuarios**

```javascript
PUT /usuarios/_doc/1
{
  "nombre": "Rick Sanchez"
}
```

- Usamos **PUT**
- Versión 1
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

- Mismo ID
- Agregamos un **nuevo campo** sobre la marcha
- Versión 2
- Result: **Updated**
- Ahora, consultemos el documento creado.

```java
GET /usuarios/_doc/1
```

- Índice: **Usuarios**
- Versión 2
- Found: **True**
- **_source** contiene el documento
- Ahora usemos **POST** para crear otro usuario

```java
POST /usuarios/_doc
{
  "nombre": "Morty",
  "apellido": "Smith"
}
```

- id: IStlI3EB3YXo6VetOVW5 (**autogenerado**)
- **Dos maneras** de crear documentos sobre un índice
- Con **POST** no tenemos que indicar ID mientras que con **PUT** si
- Para consultarlo debemos usar el id

```java
GET /usuarios/_doc/IStlI3EB3YXo6VetOVW5
```

- **Notar**: No hemos creado un índice de manera explícita
- ElasticSearch **por defecto** crea uno si no existe
- **Infiere** el tipo de dato de los campos que vayamos agregando
- Podemos **agregar u omitir** campos al crear un documento
- Esto nos permite comenzar a **trabajar de inmediato** sin definir absolutamente nada
- Ahora miremos cómo agregar **múltiples documentos** en una sola consulta
- Vamos a crear el archivo **usuarios.json** con el siguiente contenido

```java
{ "index" : { "_id" : "3" } }
{ "nombre" : "Beth", "apellido": "Smith" }
{ "index" : { "_id" : "4" } }
{ "nombre" : "Jerry", "apellido": "Smith" }
```

- En Postman, vamos a seleccionar **binary** para especificar un archivo, y luego procedemos a seleccionar **usuario**.json dentro de **curso-elastic-platzi**
- Por último, vamos a hacer una consulta a la siguiente url

```java
POST /usuarios/_bulk
```

- **Errors**: False
- **Items**: Lista de resultados para cada uno de los documentos
- Result: **Created (para todos)**
