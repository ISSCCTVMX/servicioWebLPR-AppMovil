Servicio Web LPR ISS

Versión 3.1 (uso interno)

Descripción completa del servicio:

***Ruta “/set-view?reconocedores=alta”

•	Usa como único parámetro “reconocedores” y como único valor posible “alta”
•	Despliega  todos los reconocedores de LPR
•	Ejemplo de respuesta:
{
    "notificacion": "reconocedores",
    "structure": [
        {
            "nombre": "Reconocedor de placas 2",
            "id": "2"
        },
        {
            "nombre": "Reconocedor de placas 1",
            "id": "1"
        }
    ],
    "recepcion": "ok",
    "guid": "4cb6937e-9a3e-4fb9-8ad0-fafffaf19214"
}



***Ruta “/set-alta?placa=XXXXXX&folioIncidente=123456789&database=blacklist”
        “/set-alta?placa=XXXXXX&folioIncidente=123456789&database=whitelist”

•	Usa como parámetros “placa” que debe llevar cualquier valor alfanumérico en minúsculas o mayúsculas, el parámetro “database”, y como parámetro opcional “folioIncidente”
•	Si el parámetro database es “blacklist”, se agregará a la base de datos lista negra
•	Si el parámetro database es “whitelist”, se agregará a la base de datos lista blanca
•	Ejemplo de respuesta:
{
    "recepcion": "ok",
    "guid": "3e8e7854-b7db-4218-af66-0e3cb3f8dfa8"
}
{
    "recepcion": "nok",
    "guid": "3e8e7854-b7db-4218-af66-0e3cb3f8dfa8"
}



***Ruta “/set-baja?placa=XXXXXX&database=whitelist”
        “/set-baja?placa=XXXXXX&database=blacklist”

•	Usa como parámetros “placa” que debe llevar cualquier valor alfanumérico en minúsculas o mayúsculas, el parámetro “database”
•	Si el parámetro database es “blacklist”, se eliminará de la base de datos lista negra
•	Si el parámetro database es “whitelist”, se eliminará de la base de datos lista blanca
•	Ejemplo de respuesta:
{
    "recepcion": "ok",
    "guid": "3e8e7854-b7db-4218-af66-0e3cb3f8dfa8"
}
{
    "recepcion": "nok",
    "guid": "3e8e7854-b7db-4218-af66-0e3cb3f8dfa8"
}


***Ruta “/get-plate?placa=XXXXXX&&fechaInicio=YYYYMMDDTHHMISS&fechaFin= YYYY-MM-DD HH-MI-SS&idArco=X&justDate=boolean”

•	Usa como parámetros:
o	“placa” que debe llevar cualquier valor alfanumérico en minúsculas o mayúsculas
o	“fechaInicio” que lleva un formato estándar de fecha ISO8601*
o	“fechaFin” que lleva un formato estándar de fecha ISO8601*
o	“idArco” que lleva un valor numérico entero del id del  reconocedor para hacer filtro.
o	“justDate” valor booleano (true, false). Si el valor es “true”, no incluirá la imagen en la consulta, de lo contrario retornará todos los datos con imagen.
o	Hace una búsqueda de la placa en base de datos


***NOTA: EL ÚNICO VALOR NECESARIO PARA EL SERVICIO ES “placa”, EN DADO CASO SE ENVIARÁN MÁXIMO 100 RESULTADOS ORDENADOS DEL MÁS VIEJO AL MÁS RECIENTE EN UN LAPSO DE 30 DÍAS HACIA ATRÁS DESDE EL MOMENTO DE LA CONSULTA EN TODOS LOS ARCOS.
PARA ESTA BÚSQUEDA, LA PLACA SE PUEDE ENVIAR INCOMPLETA, EL SERVICIO BUSCARÁ PLACAS QUE CUMPLAN CON LA PLACA COMO PARCIALMENTE SE HIZO LA BÚSQUEDA.

•	Ejemplos de respuesta:
{
    "structure": [
        {
            "tid": "34597",
            "nombre": "Reconocedor de placas 1",
            "timeStamp": "Mon Jun 26 10:15:24 CDT 2017",
            "placa": "843SNB",
            "direccion": "Acercamiento",
            "comentario": "Placa Test",
            "imagen": "BASE64 IMAGE",
            "recepcion": "ok",
            "guid": "b6871b03-6f27-4635-a6a2-208f816d2527"
        },
        {
            "tid": "34616",
            "nombre": "Reconocedor de placas 1",
            "timeStamp": "Mon Jun 26 10:15:35 CDT 2017",
            "placa": "846XTD",
            "direccion": "Acercamiento",
            "comentario": "null",
            "imagen": "BASE 64 IMAGE",
            "recepcion": "ok",
            "guid": "b6871b03-6f27-4635-a6a2-208f816d2527"
        }
    ]
}
{
    "structure": [
        {
            "tid": "34597",
            "nombre": "Reconocedor de placas 1",
            "timeStamp": "Mon Jun 26 10:15:24 CDT 2017",
            "placa": "843SNB",
            "direccion": "Acercamiento",
            "comentario": "Placa Test",
            "recepcion": "ok",
            "guid": "98388161-fb17-42f9-a849-4431f1f4c825"
        },
        {
            "tid": "34616",
            "nombre": "Reconocedor de placas 1",
            "timeStamp": "Mon Jun 26 10:15:35 CDT 2017",
            "placa": "846XTD",
            "direccion": "Acercamiento",
            "comentario": "null",
            "recepcion": "ok",
            "guid": "98388161-fb17-42f9-a849-4431f1f4c825"
        }
    ]
}



***Ruta “/get-whitelist”
•	No usa parámetros
•	Responde todas las placas en lista blanca
•	Ejemplo de respuesta:
{
    "placas": [
        "MRT1368"
    ],
    "recepcion": "ok",
    "guid": "87c1a3f9-a0a1-4fe6-b476-860bda1c4d4a"
}





***Ruta “/get-blacklist”
•	No usa parámetros
•	Responde todas las placas en lista negra
•	Ejemplo de respuesta:
{
    "placas": [
        "MRT1368",
        "ABC321"
    ],
    "recepcion": "ok",
    "guid": "87c1a3f9-a0a1-4fe6-b476-860bda1c4d4a"
}


***Ruta “/insert-comments?comentario=Placa Test&id=34597”
•	Inserta un comentario en el registro de LPR especificado
•	Usa como parámetros:
•	“comentario”, donde va el texto que se quiere insertar
•	“id”: que es el id de la lectura en base de datos, este dato aparece en las consultas del servicio “/get-plate”
•	Ejemplo de respuesta:
{
    "recepcion": "ok",
    "guid": "3e928866-02d8-4cdf-acea-34c2dae4a116"
}


Para todos los servicios si se hace la petición sin los datos mínimos necesarios, se retornará el siguiente error en la consulta:
{
    "notificacion": "Error",
    "descripcion": "Ingreso erroneo de datos"
}


 

***Actualización para aplicación móvil:

Los requerimientos adicionales del servicio para su funcionamiento con la aplicación móvil son los siguientes:

•	Agregar coordenadas al query y base de datos
