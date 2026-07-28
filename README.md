<p align="center">
  <img width="1024" height="369" alt="Fraudebot Logo" src="https://github.com/user-attachments/assets/c299de42-2ed9-4c5e-939c-089a8743ce20" />  
</p>
<p align="center">
    <em>Fraudebot, plataforma para consultar información de vendedores online y evitar estafas</em>
</p>

---

  **Lider de proyecto**: [Oscar Noel Cedano Beltran](https://www.linkedin.com/in/oscarced/)
  **Facebook**: [Página Oficial](https://www.facebook.com/profile.php?id=61570676484882)

---

Fraudebot es una plataforma con la cual los usuarios pueden buscar si un vendedor ha sido reportado como estafador.

Las principales características son:

- **Busqueda Multimodal**: Se puede buscar por los 16 digitos de una tarjeta debito/crédito, CLABE interbancaria, código BIC/SWITF, nombre completo, URL de perfil de Facebook/Instagram/Telegram/Página, número de teléfono.
- **Orientación jurídica**: En nuestra plataforma puedes encontrar guías para que puedas formalizar tu denuncia legalmente.
- **Bot de Whatsapp/Telegram**: Muy pronto se tendrá soporte en un bot automatizado para que puedas consultar los datos del vendedor.

*Este proyecto está basado en el proyecto sin anime de lucro [Fraudebot](https://www.facebook.com/estafabotmx) que actualmente se encuentra inactivo.*

## Desarrollo local

Coloca los tres repositorios como directorios hermanos:

```text
repos/
├── fraudebot-backend/
├── fraudebot-docker/
└── fraudebot-frontend/
```

Docker Compose instala las dependencias, crea la clave de Laravel y ejecuta las
migraciones al iniciar. No se requieren archivos de configuración para usar los
valores locales predeterminados.

```bash
cd fraudebot-docker
cp .env.example .env

# Ajusta estos valores al usuario del host para conservar permisos correctos.
sed -i "s/^FRAUDEBOT_UID=.*/FRAUDEBOT_UID=$(id -u)/" .env
sed -i "s/^FRAUDEBOT_GID=.*/FRAUDEBOT_GID=$(id -g)/" .env

docker compose up --build
```

Servicios disponibles:

- Frontend: <http://localhost>
- API: <http://localhost:9000/api/public>
- Healthcheck: <http://localhost:9000/api/public/healthcheck>
- MySQL: `localhost:3306`
- Redis: `localhost:6379`

El frontend envía las solicitudes `/api` al servicio web de Laravel dentro de
la red de Compose, por lo que no necesita configuración CORS para desarrollo.
Las credenciales de MySQL se pueden cambiar en `.env`; consulta
`.env.example`.

Para detener el stack:

```bash
docker compose down
```

Agrega `--volumes` solamente si también quieres eliminar los datos locales.
