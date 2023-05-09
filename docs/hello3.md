# Implementa con Java

Aquí aprenderás como implementar la Api en el lenguaje de programación Java.

### Envía mensajes

```bash
import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.HashMap;
import java.util.Map;

public class WhatsAppSender {

    public static void main(String[] args) throws Exception {
        // Parámetros de la solicitud
        Map<String, String> params = new HashMap<>();
        params.put("token", "ffbb639ee101fdcc0c7f82afb3c69f93");
        params.put("id", "7955");
        params.put("type", "text");
        params.put("body", "mensaje de ejemplo");
        params.put("recipient", "3166746160");

        // URL de la API de Whatsive
        String url = "https://api.whatsive.com/api/v1/sendMessage/";

        // Crear conexión HTTP
        URL obj = new URL(url);
        HttpURLConnection con = (HttpURLConnection) obj.openConnection();

        // Configurar el método de solicitud y los encabezados
        con.setRequestMethod("POST");
        con.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");

        // Formatear los parámetros y escribirlos en el cuerpo de la solicitud
        StringBuilder postData = new StringBuilder();
        for (Map.Entry<String, String> param : params.entrySet()) {
            if (postData.length() != 0) postData.append('&');
            postData.append(param.getKey());
            postData.append('=');
            postData.append(param.getValue());
        }
        byte[] postDataBytes = postData.toString().getBytes("UTF-8");
        con.setRequestProperty("Content-Length", String.valueOf(postDataBytes.length));
        con.setDoOutput(true);
        try (DataOutputStream wr = new DataOutputStream(con.getOutputStream())) {
            wr.write(postDataBytes);
        }

        // Leer la respuesta del servidor
        int responseCode = con.getResponseCode();
        BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
        String inputLine;
        StringBuilder response = new StringBuilder();
        while ((inputLine = in.readLine()) != null) {
            response.append(inputLine);
        }
        in.close();

        // Imprimir la respuesta del servidor
        System.out.println(response.toString());
    }

}

```

### Envío de contactos

```bash
import java.io.BufferedReader;
import java.io.DataOutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.HashMap;
import java.util.Map;

public class WhatsAppSender {

    public static void main(String[] args) throws Exception {
        // Parámetros de la solicitud
        Map<String, String> params = new HashMap<>();
        params.put("token", "ffbb639ee101fdcc0c7f82afb3c69f93");
        params.put("id", "7955");
        params.put("type", "contact");
        params.put("contact", "mensaje de ejemplo");
        params.put("recipient", "3166746160");

        // URL de la API de Whatsive
        String url = "https://api.whatsive.com/api/v1/sendMessage/";

        // Crear conexión HTTP
        URL obj = new URL(url);
        HttpURLConnection con = (HttpURLConnection) obj.openConnection();

        // Configurar el método de solicitud y los encabezados
        con.setRequestMethod("POST");
        con.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");

        // Formatear los parámetros y escribirlos en el cuerpo de la solicitud
        StringBuilder postData = new StringBuilder();
        for (Map.Entry<String, String> param : params.entrySet()) {
            if (postData.length() != 0) postData.append('&');
            postData.append(param.getKey());
            postData.append('=');
            postData.append(param.getValue());
        }
        byte[] postDataBytes = postData.toString().getBytes("UTF-8");
        con.setRequestProperty("Content-Length", String.valueOf(postDataBytes.length));
        con.setDoOutput(true);
        try (DataOutputStream wr = new DataOutputStream(con.getOutputStream())) {
            wr.write(postDataBytes);
        }

        // Leer la respuesta del servidor
        int responseCode = con.getResponseCode();
        BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
        String inputLine;
        StringBuilder response = new StringBuilder();
        while ((inputLine = in.readLine()) != null) {
            response.append(inputLine);
        }
        in.close();

        // Imprimir la respuesta del servidor
        System.out.println(response.toString());
    }

}
```

### Envío de contactos

```bash
import okhttp3.*;

import java.io.File;
import java.io.IOException;

public class WhatsiveApi {
    public static void main(String[] args) throws IOException {
        // Parámetros de la solicitud
        OkHttpClient client = new OkHttpClient().newBuilder()
                .build();

        MediaType mediaType = MediaType.parse("text/plain");

        RequestBody body = new MultipartBody.Builder().setType(MultipartBody.FORM)
                .addFormDataPart("token", "36755bea23b6ab44eed9037dbf6277e8")
                .addFormDataPart("id", "8731")
                .addFormDataPart("type", "media")
                .addFormDataPart("recipient", "573135775378")
                .addFormDataPart("body", "Mensaje de ejemplo con archivo adjunto")
                .addFormDataPart("file", "example.jpg",
                        RequestBody.create(MediaType.parse("application/octet-stream"),
                                new File("./example.jpg")))
                .build();
        Request request = new Request.Builder()
                .url("https://api.whatsive.com/api/v1/sendMessage/")
                .method("POST", body)
                .build();
        Response response = client.newCall(request).execute();
        System.out.println(response.body().string());
    }
}

```
