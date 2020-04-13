# Clase 05 - Verbos HTTP
- Vamos a mirar el uso de los verbos HTTP dentro de ElasticSearch

## **GET**
- Obtener un documento
- Realizar una búsqueda 
- Ver el mapeo del índice
- Entre otras

```java
GET /usuarios/_search
```

- `_search` para búsquedas en un índice
- **took**: tiempo de la consulta
- Si queremos obtener el documento sin metadata, usamos `_source`

```java
GET /usuarios/_source/1
```

- Ahora miremos el mapeo del índice

```java
GET /usuarios/_mapping
```

- El mapeo es la definición de cómo van a ser almacenados los documentos dentro de un índice
- ElasticSearch lo crea **por defecto** si no se especifica
- En este caso tenemos dos campos de tipo **text: nombre y apellido**
- **Más adelante** hablaremos en detalle de su funcionamiento

## **POST / PUT**

- En la **Clase pasada** *creamos y actualizamos* documentos
- Sin embargo, la actualización directamente usando **`_doc`** sobreescribe el documento
- Actualicemos el usuario 1: **edad=60**

```java
PUT /usuarios/_doc/1
{
    "edad": 60
}
```

- Ahora consultemos el documento

```java
GET /usuarios/_doc/1
```

- **nombre/apellido** han desaparecido
- Solo quedad **edad**
- La operación es una **indexación**, no una **actualización**
- Para actualizar una parte del documento hacemos un **POST** a **`_update`**

```java
POST /usuarios/_update/1
{
	"doc": {
	    "nombre": "Rick",
	    "apellido": "Sanchez",
	    "edad": 50
	}
}
```

```java
GET /usuarios/_doc/1
```

## **DELETE**
- Borrar **documentos o índices**
- Borremos el documento con ID 1

```java
DELETE /usuarios/_doc/1
```

- Result: **Deleted**
- Vamos a crear un **índice de prueba** para poder borrarlo

```java
POST /usuarios_deprecated/_doc
{
	"nombre": "deprecated"
}
```

- Y ahora lo **borramos**

```java
DELETE /usuarios_deprecated
```
- **Acknowledged**: True



