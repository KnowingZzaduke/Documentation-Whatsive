# Implementa con Node.js

Aquí aprenderás a implementar la Api con el lenguaje de programación Node.js

### Envío de mensajes

```bash
const https = require('https');

// Parámetros de la solicitud
const params = JSON.stringify({
  "token": "ffbb639ee101fdcc0c7f82afb3c69f93",
  "id": "7955",
  "type": "text",
  "body": "mensaje de ejemplo",
  "recipient": "3166746160"
});

// Opciones de la solicitud
const options = {
  hostname: 'api.whatsive.com',
  path: '/api/v1/sendMessage/',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Content-Length': params.length
  }
};

// Ejecutar la solicitud
const req = https.request(options, res => {
  console.log(`statusCode: ${res.statusCode}`);

  res.on('data', d => {
    process.stdout.write(d);
  });
});

req.on('error', error => {
  console.error(error);
});

req.write(params);
req.end();

```
### Envío de contactos
```bash
const https = require('https');

// Parámetros de la solicitud
const params = JSON.stringify({
  "token": "ffbb639ee101fdcc0c7f82afb3c69f93",
  "id": "7955",
  "type": "contact",
  "contact": "mensaje de ejemplo",
  "recipient": "3166746160"
});

// Opciones de la solicitud
const options = {
  hostname: 'api.whatsive.com',
  path: '/api/v1/sendMessage/',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Content-Length': params.length
  }
};

// Ejecutar la solicitud
const req = https.request(options, res => {
  console.log(`statusCode: ${res.statusCode}`);

  res.on('data', d => {
    process.stdout.write(d);
  });
});

req.on('error', error => {
  console.error(error);
});

req.write(params);
req.end();

```

### Envío de archivos
```bash
const https = require('https');
const fs = require('fs');
const FormData = require('form-data');

// Parámetros de la solicitud
const params = {
  "token": "36755bea23b6ab44eed9037dbf6277e8",
  "id": "8731",
  "type": "media",
  "recipient": "573135775378"
};

// Archivo a enviar
const file_path = "./example.jpg";
const file_name = "example.jpg";
const file_type = mime_type(file_path);

// Agregar el archivo al objeto de parámetros
const form = new FormData();
form.append('file', fs.createReadStream(file_path), {
  filename: file_name,
  contentType: file_type,
});
form.append('body', 'Mensaje de ejemplo con archivo adjunto');

for (const [key, value] of Object.entries(params)) {
  form.append(key, value);
}

// Opciones de la solicitud
const options = {
  hostname: 'api.whatsive.com',
  path: '/api/v1/sendMessage/',
  method: 'POST',
  headers: {
    ...form.getHeaders(),
  }
};

// Ejecutar la solicitud
const req = https.request(options, res => {
  console.log(`statusCode: ${res.statusCode}`);

  res.on('data', d => {
    process.stdout.write(d);
  });
});

req.on('error', error => {
  console.error(error);
});

form.pipe(req);

```