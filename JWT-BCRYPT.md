# PASO 1 — Autenticación con roles (JWT)

## 🎯 Objetivo del paso

- Tener **usuarios reales**
- Login con **JWT**
- Roles: `cliente` y `admin`
- Base para proteger rutas después

---

## 1️⃣ Entidad `Usuario`

📁 `src/usuario/usuario.entity.ts`

```ts
import { Entity, PrimaryKey, Property, Enum } from "@mikro-orm/core";

@Entity()
export class Usuario {
  @PrimaryKey()
  id!: number;

  @Property({ unique: true })
  email!: string;

  @Property()
  passwordHash!: string;

  @Enum(() => ["cliente", "admin"])
  rol!: "cliente" | "admin";

  @Property({ default: true })
  activo!: boolean;
}
```

✔ Simple
✔ Clara
✔ Rol explícito (muy defendible)

---

## 2️⃣ Crear usuarios (seed inicial)

Para no depender del front.

📁 `src/usuario/usuario.seed.ts`

```ts
import bcrypt from "bcrypt";
import { orm } from "../shared/db/orm.js";
import { Usuario } from "./usuario.entity.js";

export async function seedUsuarios() {
  const em = orm.em.fork();

  const existe = await em.findOne(Usuario, { email: "admin@demo.com" });
  if (existe) return;

  const admin = em.create(Usuario, {
    email: "admin@demo.com",
    passwordHash: await bcrypt.hash("admin123", 10),
    rol: "admin",
  });

  const cliente = em.create(Usuario, {
    email: "cliente@demo.com",
    passwordHash: await bcrypt.hash("cliente123", 10),
    rol: "cliente",
  });

  await em.persistAndFlush([admin, cliente]);
}
```

Y lo llamás al levantar la app:

📁 `app.ts`

```ts
import { seedUsuarios } from "./usuario/usuario.seed.js";

await seedUsuarios();
```

📌 En la defensa:

> “Creamos usuarios semilla para facilitar pruebas y evaluación”.

---

## 3️⃣ Login (Auth Controller)

📁 `src/auth/auth.controller.ts`

```ts
import { Request, Response } from "express";
import bcrypt from "bcrypt";
import jwt from "jsonwebtoken";
import { orm } from "../shared/db/orm.js";
import { Cliente } from "../cliente/cliente.entity.js";
import { RolSchema } from "./auth.schema.js";

export async function login(req: Request, res: Response) {
  const { email, password } = req.body;

  const em = orm.em.fork();

  const cliente = await em.findOne(Cliente, { email });

  if (!cliente)
    return res.status(401).json({ message: "Credenciales inválidas" });

  const validPassword = await bcrypt.compare(password, cliente.passwordHash);

  if (!validPassword)
    return res.status(401).json({ message: "Credenciales inválidas" });

  // ✅ valida rol desde DB
  const rol = RolSchema.parse(cliente.rol);

  const token = jwt.sign(
    {
      clienteId: cliente.id,
      rol,
    },
    process.env.JWT_SECRET!,
    { expiresIn: "1h" },
  );

  res.json({
    token,
    cliente: {
      id: cliente.id,
      email: cliente.email,
      rol,
    },
  });
}
```

---

## 4️⃣ Ruta de login

📁 `src/auth/auth.routes.ts`

```ts
import { Router } from "express";
import { login } from "./auth.controller.js";

const router = Router();

router.post("/login", login);

export default router;
```

📁 `app.ts`

```ts
import authRouter from "./auth/auth.routes.js";

app.use("/api/auth", authRouter);
```

---

## 5️⃣ Variables de entorno (OBLIGATORIO)

📁 `.env`

```env
JWT_SECRET=supersecretjwtkey
```

📁 `.env.example`

```env
JWT_SECRET=
DB_HOST=
DB_USER=
DB_PASSWORD=
DB_NAME=
PORT=3000
```

📌 Esto **ya cumple** el requisito de ambientes.

---

## 6️⃣ Probar login (manual)

```http
POST http://localhost:3000/api/auth/login
Content-Type: application/json

{
  "email": "admin@demo.com",
  "password": "admin123"
}
```

Respuesta esperada:

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "usuario": {
    "id": 1,
    "email": "admin@demo.com",
    "rol": "admin"
  }
}
```

✔ Backend auth funcionando
✔ JWT correcto
✔ Roles listos

---

## 📌 Estado al cerrar el paso 1

✔ Usuario
✔ Login
✔ JWT
✔ Roles
✔ Variables de entorno

Todavía **NO** protegimos rutas (eso es el paso 2).

---

## 👉 Próximo paso (cuando sigamos)

**Paso 2: Middleware de autenticación + protección de rutas por rol**
Ahí cerramos uno de los requisitos más importantes del enunciado.

Cuando quieras, seguimos.
