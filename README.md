# Reseñalo — Frontend

Aplicación web para reseñar películas, videojuegos y libros (estilo Letterboxd, multi-categoría). Construida con React + Vite, consume la API REST del backend de ReviewApp.

## URLs de producción

- **Frontend:** https://review-app-frontend-pi.vercel.app
- **Backend:** https://reviewapp-backend.vercel.app

## Usuario de prueba (email ya verificado)

- **Email:** lud.14.pache@gmail.com
- **Password:** ludmi28

## Stack

- React 18 + Vite
- React Router DOM v6 (rutas y navegación)
- CSS plano con variables CSS (design tokens), sin frameworks de UI
- Context API para manejo de sesión (usuario + JWT)
- Fetch API para consumo de la API REST

## Instalación local

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/ludmipache/ReviewApp-Frontend.git
   cd ReviewApp-Frontend
   ```

2. Instalar dependencias:
   ```bash
   npm install
   ```

3. Crear un archivo `.env` en la raíz:
   ```env
   VITE_API_URL=http://localhost:3000
   ```
   En producción reemplazar por la URL pública del backend.

4. Levantar en modo desarrollo:
   ```bash
   npm run dev
   ```

5. Generar build de producción:
   ```bash
   npm run build
   ```
   Los archivos quedan en `dist/`.

## Estructura

```
src/
 ├─ api/
 │   ├─ client.js         # helper de fetch con manejo de auth y errores
 │   ├─ auth.api.js       # register, login, verifyEmail
 │   ├─ items.api.js      # CRUD de items
 │   └─ reviews.api.js    # CRUD de reviews
 ├─ components/
 │   ├─ Navbar.jsx        # barra de navegación responsiva
 │   ├─ ItemCard.jsx      # tarjeta de item para el catálogo
 │   ├─ ReviewCard.jsx    # tarjeta de reseña individual
 │   ├─ StarRating.jsx    # componente de estrellas (lectura y edición)
 │   └─ ProtectedRoute.jsx # redirige a /login si no hay sesión
 ├─ constants/
 │   └─ itemTypes.js      # labels e íconos por tipo de item
 ├─ context/
 │   └─ AuthContext.jsx   # maneja usuario logueado y token JWT
 ├─ pages/
 │   ├─ Login.jsx         # inicio de sesión
 │   ├─ Register.jsx      # registro de usuario
 │   ├─ VerifyEmail.jsx   # pantalla de verificación de email
 │   ├─ ItemsList.jsx     # catálogo con filtro por tipo
 │   ├─ ItemDetail.jsx    # detalle de item + reviews + form de reseña
 │   ├─ ItemForm.jsx      # crear / editar item
 │   └─ MyReviews.jsx     # mis reseñas con editar y borrar
 ├─ App.jsx               # definición de rutas
 └─ main.jsx              # entry point
```

## Pantallas

| Ruta | Descripción | Requiere login |
|---|---|---|
| `/` | Catálogo de items, filtrable por tipo (película / videojuego / libro) | No |
| `/login` | Inicio de sesión | No |
| `/registro` | Registro de usuario nuevo | No |
| `/verificar-email?verification_token=...` | Verificación de email desde el link del correo | No |
| `/items/:item_id` | Detalle de un item: info, reseñas y formulario para reseñar | No (reseñar sí requiere login) |
| `/items/nuevo` | Formulario para agregar un título al catálogo | Sí |
| `/items/:item_id/editar` | Formulario para editar un título existente | Sí |
| `/mis-resenas` | Listado de las reseñas propias con editar y borrar | Sí |

## Funcionalidades

- Registro de usuarios con verificación por correo electrónico
- Login con JWT — token guardado en `localStorage`
- Catálogo de películas, videojuegos y libros con filtro por categoría
- CRUD completo de Items (crear, ver, editar, eliminar) — protegido por JWT
- CRUD completo de Reviews con rating de 1 a 5 estrellas y comentario
- Un usuario puede dejar múltiples reseñas sobre el mismo item
- Solo el autor puede editar o eliminar su propia reseña
- Rutas protegidas que redirigen a `/login` si no hay sesión activa
- UI responsiva de 320px a 2000px de ancho

## Sesión

El token JWT se guarda en `localStorage` junto con los datos básicos del usuario. `AuthContext` expone `user`, `login`, `logout` y `loading` a toda la aplicación. Las rutas protegidas usan el componente `ProtectedRoute`, que redirige a `/login` si no hay sesión activa.

## Diseño

Paleta oscura inspirada en cartelera de cine: fondo `#15141a`, superficie `#1f1d27`, acento ámbar `#e8a23d`. Tipografía: `Fraunces` para títulos, `Inter` para texto. Grid responsivo de tarjetas tipo póster para el catálogo.