# PruneMate

## ¿Qué es PruneMate?

[PruneMate](https://github.com/anoniemerd/PruneMate) es una herramienta de código abierto diseñada para ayudar a mantener limpios los entornos de Docker. Su función principal es automatizar la ejecución de los comandos nativos de limpieza de Docker (`docker system prune`), lo que permite eliminar recursos no utilizados (como contenedores, imágenes, redes y volúmenes) para liberar espacio en disco.

Entre sus características principales se incluyen:
- **Interfaz Web Ligera:** Para gestionar configuraciones, ejecutar limpiezas manuales de forma segura y visualizar estadísticas del espacio recuperado.
- **Limpieza Automatizada:** Permite programar tareas de limpieza periódicas (diarias, semanales o mensuales).
- **Soporte Multi-Host:** Capacidad para gestionar múltiples hosts de Docker.
- **Notificaciones:** Integración opcional con servicios como Gotify o ntfy.sh para recibir alertas de las limpiezas.

> **⚠️ Advertencia:** Dado que PruneMate utiliza los comandos nativos de Docker, eliminará permanentemente los recursos que no estén en uso. Se recomienda verificar qué recursos serán eliminados antes de habilitar las tareas automatizadas, especialmente en el caso de volúmenes que puedan contener datos importantes.

## ¿Cómo levantar el servicio?

El proyecto incluye una configuración lista para utilizar con Docker Compose. Para levantar el servicio localmente, sigue estos pasos:

1. Ubícate en el directorio donde se encuentra la configuración de Docker Compose:
   ```bash
   cd docker-compose
   ```

2. Revisa el archivo `.env` y ajusta las variables de entorno si es necesario. Por defecto, incluye configuraciones de zona horaria y opciones para habilitar autenticación:
   ```env
   PRUNEMATE_TZ=America/Argentina/Buenos_Aires
   PRUNEMATE_TIME_24H=true
   # Opcional: Habilitar autenticación de usuario
   PRUNEMATE_AUTH_USER=admin
   PRUNEMATE_AUTH_PASSWORD_HASH=admin_base64_pass
   ```

3. (Opcional) Si necesitas acceder a la interfaz web, asegúrate de descomentar el mapeo de puertos en tu archivo `docker-compose.yml`:
   ```yaml
   ports:
     - "8080:8080"
   ```

4. Levanta el contenedor en segundo plano:
   ```bash
   docker-compose up -d
   ```

Una vez ejecutado, PruneMate estará interactuando con el socket de Docker para realizar sus tareas. Los archivos de configuración persistirán en el volumen `prunemate_config_data_volume` y los logs podrán verse en el directorio `./logs` local.

Si habilitaste el mapeo de puertos en el paso 3, podrás acceder a la interfaz web ingresando a: [http://localhost:8080](http://localhost:8080).
