# Implementa con PHP

Aquí aprenderás como implementar la Api en el lenguaje de programación PHP.

### Envío de mensajes de texto

```bash
<?php
// Parámetros de la solicitud
$params = array(
    "token" => "ffbb639ee101fdcc0c7f82afb3c69f93",
    "id" => "7955",
    "type" => "text",
    "body" => "mensaje de ejemplo",
    "recipient" => "3166746160"
);

// URL de la API de Whatsive
$url = "https://api.whatsive.com/api/v1/sendMessage/";

// Inicializar cURL
$ch = curl_init();

// Establecer opciones de cURL
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $params);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
//curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/json'));

// Ejecutar la solicitud
$response = curl_exec($ch);

// Obtener el código de respuesta HTTP
$httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);

// Cerrar la conexión cURL
curl_close($ch);

// Verificar si la solicitud se completó con éxito
echo $response;
?>
```

### Envío de contactos

```bash
<?php
// Parámetros de la solicitud
$params = array(
    "token" => "ffbb639ee101fdcc0c7f82afb3c69f93",
    "id" => "7955",
    "type" => "contact",
    "contact" => "mensaje de ejemplo",
    "recipient" => "3166746160"
);

// URL de la API de Whatsive
$url = "https://api.whatsive.com/api/v1/sendMessage/";

// Inicializar cURL
$ch = curl_init();

// Establecer opciones de cURL
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $params);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
//curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/json'));

// Ejecutar la solicitud
$response = curl_exec($ch);

// Obtener el código de respuesta HTTP
$httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);

// Cerrar la conexión cURL
curl_close($ch);

// Verificar si la solicitud se completó con éxito
echo $response;
?>
```

### Envía de archivos

```bash
<?php
// Parámetros de la solicitud
$params = array(
    "token" => "36755bea23b6ab44eed9037dbf6277e8",
    "id" => "8731",
    "type" => "media",
    "recipient" => "573135775378"
);

// Archivo a enviar
$file_path = "./example.jpg";
$file_name = "example.jpg";
$file_type = mime_content_type($file_path);

// Agregar el archivo al array de parámetros
$params["file"] = curl_file_create($file_path, $file_type, $file_name);
$params["body"] = "Mensaje de ejemplo con archivo adjunto";

// URL de la API de Whatsive
$url = "https://api.whatsive.com/api/v1/sendMessage/";

// Inicializar cURL
$ch = curl_init();

// Establecer opciones de cURL
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $params);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

// Ejecutar la solicitud
$response = curl_exec($ch);

// Obtener el código de respuesta HTTP
$httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);

// Cerrar la conexión cURL
curl_close($ch);

// Verificar si la solicitud se completó con éxito
echo $response;
?>
```
