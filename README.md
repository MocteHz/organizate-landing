# organizate-landing

Landing estático de OrganizaTe (organiza.mchtec.net): página de inicio,
registro, verificación de cuenta, reset de contraseña, tutoriales y
first-login de invitaciones.

## Arquitectura

- **Estático puro** (nginx): sin proxy de API. Todas las llamadas van
  directo a `https://backend.mchtec.net/api/...` (CORS ya configurado en
  el backend para `https://organiza.mchtec.net`).
- **Deploy**: Coolify (proyecto OrganizaTe, build pack Dockerfile,
  dominio https://organiza.mchtec.net). Push a `main` = auto-deploy.
- **APK** (`/descargas/organizate.apk`): NO está en git (101MB). Se sirve
  desde un volumen persistente de Coolify con host_path
  `/home/ubuntu/organiza-landing/descargas` → mount
  `/usr/share/nginx/html/descargas`. Actualizar el APK = copiar el archivo
  a esa ruta en el servidor.

## Páginas y rutas

| Ruta              | Archivo                |
|-------------------|------------------------|
| `/`               | index.html             |
| `/register`       | register.html          |
| `/verify`         | verify.html            |
| `/reset-password` | reset-password.html    |
| `/tutoriales`     | tutoriales.html        |
| `/auth/first-login` | auth/first-login.html |

Las rutas limpias sin `.html` las resuelve el `try_files` del nginx.conf.
