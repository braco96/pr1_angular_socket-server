
# ⚡ Socket Server (TypeScript + Node.js + Express + Socket.IO)

Servidor backend en **Node.js** con **TypeScript**, **Express** y **Socket.IO** para manejar comunicación en tiempo real entre clientes.  
Diseñado para funcionar junto a una aplicación cliente Angular que consume eventos vía WebSocket.

---

## 🚀 Características principales

- Comunicación **bidireccional** en tiempo real mediante `socket.io`.
- API REST básica para enviar mensajes desde HTTP.
- Gestión de **usuarios conectados** mediante clases y listas.
- Emisión de mensajes **públicos** y **privados** a clientes.
- **TypeScript** con tipado fuerte y estructura modular.
- Servidor Express con **CORS** y **body-parser**.

---

## 🧱 Tecnologías utilizadas

- **Node.js**
- **Express**
- **Socket.IO**
- **TypeScript**
- **Nodemon** (para desarrollo)
- **CORS / Body-Parser**

---

## 📦 Instalación

1. **Clonar el repositorio**  
   ```bash
   git clone https://github.com/tuusuario/socket-server.git
   cd socket-server
   ```

2. **Instalar dependencias**
   ```bash
   npm install
   ```

3. **Compilar TypeScript en modo observación**
   ```bash
   tsc -w
   ```

4. **Levantar el servidor**
   ```bash
   nodemon dist/
   # o
   node dist/
   ```

---

## ⚙️ Configuración

El archivo de configuración principal está en:

```ts
// global/environment.ts
export const SERVER_PORT: number = Number(process.env.PORT) || 5000;
```

Puedes definir el puerto desde variables de entorno (`PORT`) o usar el valor por defecto (`5000`).

---

## 🧩 Estructura del proyecto

```
socket-server/
├── classes/
│   ├── server.ts           # Configuración del servidor Express y Socket.IO
│   ├── usuario.ts          # Clase modelo de usuario
│   └── usuarios-lista.ts   # Lista de usuarios conectados
│
├── sockets/
│   └── socket.ts           # Lógica de conexión, mensajes, desconexión y configuración de usuarios
│
├── routes/
│   └── router.ts           # Endpoints REST (mensajes HTTP)
│
├── global/
│   └── environment.ts      # Variables globales (puerto)
│
├── index.ts                # Punto de entrada de la aplicación
├── package.json
├── tsconfig.json
└── README.md
```

---

## 🧠 Arquitectura y flujo de datos

```text
Cliente WebSocket (Angular)
        │
        ▼
[Socket.IO en Node.js]
        │
        ├── Conexión → socket.conectarCliente()
        ├── Configuración de usuario → socket.configurarUsuario()
        ├── Mensajes → socket.mensaje()
        └── Desconexión → socket.desconectar()
```

---

## 🌐 Endpoints HTTP disponibles

### 1️⃣ GET `/mensajes`
**Descripción:** Prueba básica de conexión.

**Respuesta:**
```json
{
  "ok": true,
  "mensaje": "Todo esta bien!!"
}
```

---

### 2️⃣ POST `/mensajes`
**Descripción:** Envía un mensaje público a todos los clientes.

**Body:**
```json
{
  "de": "Luis",
  "cuerpo": "Hola a todos"
}
```

**Respuesta:**
```json
{
  "ok": true,
  "cuerpo": "Hola a todos",
  "de": "Luis"
}
```

---

### 3️⃣ POST `/mensajes/:id`
**Descripción:** Envía un mensaje privado a un cliente específico.

**Parámetros de ruta:**
- `id`: ID del socket del cliente destino.

**Body:**
```json
{
  "de": "Luis",
  "cuerpo": "Mensaje privado"
}
```

**Respuesta:**
```json
{
  "ok": true,
  "cuerpo": "Mensaje privado",
  "de": "Luis",
  "id": "socketId"
}
```

---

## 👥 Manejo de usuarios conectados

Ubicado en `classes/usuarios-lista.ts`:

- `agregar(usuario: Usuario)` → Añade un usuario nuevo.  
- `actualizarNombre(id, nombre)` → Cambia el nombre asociado a un socket.  
- `getLista()` → Retorna todos los usuarios.  
- `getUsuario(id)` → Devuelve un usuario específico.  
- `getUsuariosEnSala(sala)` → Filtra por sala.  
- `borrarUsuario(id)` → Elimina usuario desconectado.

---

## 🔄 Integración con el cliente Angular

El cliente Angular se conecta a este servidor usando `ngx-socket-io` apuntando a la URL definida en su `environment.wsUrl`, que debe coincidir con el puerto configurado aquí (por defecto `http://localhost:5000`).

Eventos manejados en común:
- `mensaje`
- `mensaje-nuevo`
- `mensaje-privado`
- `configurar-usuario`

---

## 🧪 Scripts útiles

```bash
# Instalar dependencias
npm install

# Compilar TypeScript
tsc -w

# Levantar servidor
nodemon dist/

# Limpiar salida anterior
rm -rf dist
```

---

## 🧰 Recomendaciones

- Usa **Nodemon** para reinicios automáticos en desarrollo.
- Usa **pm2** o **Docker** para despliegue en producción.
- Para entornos HTTPS, configura `server.ts` con `https.createServer()`.

---

## 📜 Licencia

MIT — Puedes modificar y distribuir libremente.

---

© 2025 Luisito Bravete — Backend para chat en tiempo real.
