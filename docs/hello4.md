# Implementa con Python

Aquí aprenderás como implementar la Api en el lenguaje de programación Python.

### Envío de mensajes

```bash
import requests

# Parámetros de la solicitud
params = {
    "token": "ffbb639ee101fdcc0c7f82afb3c69f93",
    "id": "7955",
    "type": "text",
    "body": "mensaje de ejemplo",
    "recipient": "3166746160"
}

# URL de la API de Whatsive
url = "https://api.whatsive.com/api/v1/sendMessage/"

# Realizar la solicitud POST con los parámetros
response = requests.post(url, data=params)

# Obtener el código de respuesta HTTP
httpCode = response.status_code

# Verificar si la solicitud se completó con éxito
print(response.text)


```

### Envío de contactos

```bash
import requests

# Parámetros de la solicitud
params = {
    "token": "ffbb639ee101fdcc0c7f82afb3c69f93",
    "id": "7955",
    "type": "contact",
    "contact": "mensaje de ejemplo",
    "recipient": "3166746160"
}

# URL de la API de Whatsive
url = "https://api.whatsive.com/api/v1/sendMessage/"

# Realizar la solicitud POST con los parámetros
response = requests.post(url, data=params)

# Obtener el código de respuesta HTTP
httpCode = response.status_code

# Verificar si la solicitud se completó con éxito
print(response.text)


```

### Envío de archivos

```bash
import requests

# Parámetros de la solicitud
params = {
    "token": "36755bea23b6ab44eed9037dbf6277e8",
    "id": "8731",
    "type": "media",
    "recipient": "573135775378",
}

# Archivo a enviar
file_path = "./example.jpg"
file_name = "example.jpg"
file_type = mimetypes.guess_type(file_path)[0]

# Agregar el archivo al diccionario de parámetros
with open(file_path, "rb") as file:
    params["file"] = (file_name, file, file_type)
    params["body"] = "Mensaje de ejemplo con archivo adjunto"

# URL de la API de Whatsive
url = "https://api.whatsive.com/api/v1/sendMessage/"

# Ejecutar la solicitud
response = requests.post(url, files=params)

# Obtener el código de respuesta HTTP
http_code = response.status_code

# Verificar si la solicitud se completó con éxito
print(response.text)

```
