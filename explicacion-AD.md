Excelente, ahora estamos hablando en **modo aprobación directa**.
Te voy a ordenar todo **desde backend**, con decisiones concretas y sin humo, para que _cada punto del enunciado quede cubierto y defendible_.

Voy por partes y al final te dejo un **plan de ejecución**.

---

# 1️⃣ Tests automatizados (unidad + integración)

### 📌 Requisito

- 1 test automatizado **por integrante**
- 1 test de **integración**

### 🔧 Stack recomendado (Node + Express + MikroORM)

Usá **Vitest** (más simple que Jest con Vite/TS):

```bash
npm install -D vitest supertest
```

En `package.json`:

```json
{
  "scripts": {
    "test": "vitest run",
    "test:watch": "vitest"
  }
}
```

---

## 🧪 Test unitario (ejemplo defendible)

👉 Testear **lógica de negocio pura**, no Express.

Ejemplo: transición de estados del pedido.

```ts
// src/pedido/pedido.estado.test.ts
import { describe, it, expect } from "vitest";

const transiciones = {
  pendiente: ["confirmado", "cancelado"],
  confirmado: ["pagado", "cancelado"],
  pagado: ["enviado"],
  enviado: ["entregado"],
  entregado: [],
  cancelado: [],
};

function puedeTransicionar(actual: string, nuevo: string) {
  return transiciones[actual]?.includes(nuevo);
}

describe("Estados de Pedido", () => {
  it("permite pasar de pendiente a confirmado", () => {
    expect(puedeTransicionar("pendiente", "confirmado")).toBe(true);
  });

  it("no permite pasar de pendiente a enviado", () => {
    expect(puedeTransicionar("pendiente", "enviado")).toBe(false);
  });
});
```

✔ Fácil
✔ Lógica real
✔ Totalmente justificable

---

## 🌐 Test de integración (Express + DB)

👉 Testear **POST /api/pedidos**

```ts
// src/pedido/pedido.integration.test.ts
import request from "supertest";
import app from "../app";

describe("POST /api/pedidos", () => {
  it("crea un pedido correctamente", async () => {
    const res = await request(app)
      .post("/api/pedidos")
      .send({
        cliente: 2,
        items: [{ mueble: 1, cantidad: 1 }],
      });

    expect(res.status).toBe(201);
    expect(res.body.data.total).toBeGreaterThan(0);
  });
});
```

📌 Para la defensa:

> “Este test valida la integración entre routing, controller, ORM y base de datos”.

---

# 2️⃣ Login + autenticación + roles

### 📌 Requisito

- Login propio o third-party
- Al menos **2 niveles de acceso**
- Protección de rutas

### ✅ Solución clara y defendible

**JWT + roles**

Roles:

- `cliente`
- `admin`

---

## 🧑‍💻 Entidad Usuario

```ts
// src/usuario/usuario.entity.ts
@Enum(() => ["cliente", "admin"])
rol!: "cliente" | "admin";

@Property()
email!: string;

@Property()
passwordHash!: string;
```

---

## 🔐 Login

```ts
// POST /api/auth/login
const token = jwt.sign(
  { userId: user.id, rol: user.rol },
  process.env.JWT_SECRET!,
  { expiresIn: "1h" },
);
```

---

## 🛡 Middleware de autenticación

```ts
export function auth(requiredRoles: Array<"cliente" | "admin">) {
  return (req, res, next) => {
    const token = req.headers.authorization?.split(" ")[1];
    if (!token) return res.status(401).json({ message: "No token" });

    const payload = jwt.verify(token, process.env.JWT_SECRET!) as any;

    if (!requiredRoles.includes(payload.rol)) {
      return res.status(403).json({ message: "Forbidden" });
    }

    req.user = payload;
    next();
  };
}
```

---

## 🔒 Protección de rutas (ejemplo)

```ts
pedidoRouter.post("/", auth(["cliente"]), crearPedido);
pedidoRouter.patch("/:id/estado", auth(["admin"]), updateEstadoPedido);
```

📌 Defensa perfecta:

> “Separamos responsabilidades entre cliente y administrador, protegiendo las rutas según rol”.

---

# 3️⃣ Ambientes (.env)

### 📌 Requisito

Definir ambientes correctamente.

### ✅ Tu enfoque con dotenv está bien, solo hay que **ordenarlo**

```bash
.env
.env.test
.env.example
```

```ts
import dotenv from "dotenv";
dotenv.config({ path: process.env.NODE_ENV === "test" ? ".env.test" : ".env" });
```

Variables mínimas:

```env
DB_HOST=
DB_USER=
DB_PASSWORD=
DB_NAME=
JWT_SECRET=
PORT=3000
```

✔ Muy defendible
✔ Profesional

---

# 4️⃣ CRUDs completos (backend)

Ya tenés:

- ✔ Mueble
- ✔ Pedido
- ✔ Item
- ✔ Cliente

Solo asegurate de:

- `GET / POST / PUT / DELETE` en al menos:
  - Mueble
  - Cliente

Aunque el front no los use todos, **el backend debe tenerlos**.

---

# 5️⃣ Casos de uso / Epics (CLAVE)

Tenés mínimo **2 relacionados**:

### 🧩 CU1 – Cliente realiza compra

- Selecciona muebles
- Crea pedido
- Genera items y total

### 🧩 CU2 – Administrador gestiona pedidos

- Lista pedidos
- Cambia estado (`confirmado`, `pagado`, etc.)

📌 Relación clara:

> El pedido creado por el cliente es input del caso de uso del administrador.

Esto **cumple exacto** el requisito.

---

# 6️⃣ Entregables (backend)

### 📄 Documentación API

Usá **OpenAPI / Swagger**:

```bash
npm install swagger-ui-express yamljs
```

Un `openapi.yaml` con:

- `/auth/login`
- `/pedidos`
- `/muebles`

---

### 🧪 Evidencia de tests

- Screenshot de:

```bash
npm run test
```

---

### 📘 README (checklist)

- `npm install`
- `npm run dev`
- variables de entorno
- credenciales demo:
  - [admin@demo.com](mailto:admin@demo.com) / admin123
  - [cliente@demo.com](mailto:cliente@demo.com) / cliente123

---

# 🧭 Plan de ejecución recomendado

Orden **óptimo** (no improvises):

1. Agregar Usuario + Auth + Roles
2. Proteger rutas
3. Agregar tests (unitario + integración)
4. Completar CRUDs faltantes
5. Swagger
6. README + scripts
7. Deploy

---

Si querés, en el próximo mensaje hacemos **paso 1 completo**:
👉 diseño final de `Usuario`, `auth`, `login` y middlewares **con código listo para pegar**.

Decime y arrancamos.
