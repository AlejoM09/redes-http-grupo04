# Laboratorio HTTP – Grupo 04

Sitio web hecho 100 % con HTML, organizado en GitHub y desplegable con Docker.
Actividad práctica de la **capa 7 (aplicación) del modelo OSI** del curso
**Internet: redes y comunicaciones IP**, Universidad de Ibagué, 2026B. Docente: Daniel Palomo.

## Integrantes

| Integrante | Página |
|---|---|
| Alejandro Marín Aguilar | `integrantes/alejandro.html` |
| Misael Gallo Tangarife | `integrantes/misael.html` |
| Nelson Garzón Soleto | `integrantes/nelson.html` |

Cada integrante tiene una biografía breve y un resumen de lo aprendido en el curso.

## Estructura del repositorio

```text
.
├── README.md
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── .gitignore
├── index.html
├── css/
│   └── style.css
├── img/
│   ├── osi-capas.svg
│   └── avatar-*.svg
└── integrantes/
    ├── alejandro.html
    ├── misael.html
    └── nelson.html
```

## Requisitos

- [Git](https://git-scm.com/)
- [Docker](https://docs.docker.com/get-docker/) con el plugin Docker Compose

No se necesita cuenta en Docker Hub: la imagen se construye en local.

## Cómo replicar el sitio en otra máquina

1. Clonar el repositorio:

   ```bash
   git clone https://github.com/AlejoM09/redes-http-grupo04.git
   cd redes-http-grupo04
   ```

2. Construir y levantar el contenedor:

   ```bash
   docker compose up -d --build
   ```

3. Abrir el sitio en el navegador:

   ```text
   http://localhost:8001
   ```

### Alternativa sin Docker Compose

```bash
docker build -t sitio-html-grupo04 .
docker run -d -p 8001:80 --name sitio-html-grupo04 sitio-html-grupo04
```

## Comandos útiles

| Acción | Comando |
|---|---|
| Ver el estado | `docker compose ps` |
| Ver los logs | `docker compose logs -f` |
| Detener el servicio | `docker compose down` |
| Reconstruir desde cero | `docker compose down && docker compose up -d --build` |

## Cómo funciona

- El `Dockerfile` parte de `nginx:alpine`, copia el sitio a `/usr/share/nginx/html` y expone el puerto 80.
- `docker-compose.yml` publica el puerto 80 del contenedor en el **8001** de la máquina.
- Las páginas declaran `<meta charset="utf-8">` para que los caracteres con tilde se vean bien.

## Verificar que HTTP está funcionando

Con el contenedor arriba, se puede ver una respuesta HTTP real desde la terminal:

```bash
curl -I http://localhost:8001
```

Debe responder `HTTP/1.1 200 OK` con la cabecera `Server: nginx`.
También se puede abrir el navegador, pulsar `F12` y revisar la pestaña **Red** para ver las peticiones y los códigos de estado.

## Licencia

Uso académico y educativo.
