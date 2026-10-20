# Plantillas React v2: LOGIN e HISTORIAL

> Todo es genérico: no hay nombres de ningún modelo. Las hojas impresas en tus palabras (una por modelo) se hacen al final.
> Al final del documento está **"Qué se probó y qué no"**.

## 0. Qué cambió respecto de la versión anterior

- **El HTML ya no viene a medio armar.** Donde va HTML hay **una sola marca `PEGAR ACÁ`** que dice **de qué archivo viejo sale, qué buscar y desde dónde hasta dónde**. Lo pegás y lo traducís vos.
- **Debajo de cada marca hay un PROVISORIO que ya anda.** Con solo copiar y reemplazar tokens, la app compila y funciona entera: rutas, datos, login o historial, 404. Se ve feo, pero anda. El HTML se pega al final para que quede lindo.
- **Los nombres salen de la rúbrica** (`XxxCard`, `useXxx`, `XxxRecientesContext`). Si la rúbrica no los dice, los elegís vos.
- **HISTORIAL ya no tiene bloques ▼/▲ adentro de los archivos.** Hay versiones enteras para elegir: **sin filtros** o **con filtros**, y **recientes como lista** o **recientes cruzando con la API**.
- **Menos tokens:** HISTORIAL pasó de 19 a 16 (11 si no hay filtros). LOGIN sigue con 8.

---

## 1. El día del examen: orden de trabajo (de lo más fácil a lo más difícil)

| Paso | Qué hacés | Cuánto hay que pensar |
|---|---|---|
| **0. Previos** | 1) Leer README, rúbrica y `server/*.js` → **familia** (sección 3). 2) En `react/src/` borrar todo menos `main.jsx`. 3) `react/src/index.css` = el CSS de la carpeta `css/` del viejo + al final `a { text-decoration: none; color: inherit; }`. 4) En `react/index.html`: copiar los `<link …>` del `<head>` del `index.html` viejo, y si el `<body>` viejo tiene `class="…"`, ponérselo al `<body>` de `react/index.html`. 5) `npm install` en `server/` y en `react/`. | Nada |
| **1. COPIAR** | Los archivos que dicen `PASO 1 · COPIAR` arriba de todo. No se tocan. | Nada |
| **2. REEMPLAZAR** | Llenar la **ficha de tokens** (sección 4) y hacer Ctrl+H en los archivos `PASO 2`. En `HomePage.jsx` (LOGIN) elegir **una** de las 3 líneas de OPCIÓN. Al final, **Ctrl+Shift+F `__` en `react/src` tiene que dar 0**. | Buscar datos en el servidor y la rúbrica |
| **3. PROBAR** | Terminal 1: `cd server` → `npm start`. Terminal 2: `cd react` → `npm run dev`. Probá: la lista, entrar a uno, volver, una dirección inventada (404), y el login o los recientes. **Si esto anda, ya tenés casi todo lo que la rúbrica puntúa como funcionamiento.** | Nada |
| **4. PEGAR HTML** | Recorrer las marcas `PEGAR ACÁ` en este orden: **header → tarjeta → home (grupo o pantalla de inicio) → recientes → detalle** (el detalle va último porque es el más largo). Después de **cada** pegada, mirá el navegador: si se rompió y no sale, Ctrl+Z hasta volver al provisorio. **Nunca entregues algo que no compila.** | Encontrar el HTML (sección 6) y traducirlo |
| **5. Si sobra tiempo** | Clases y textos chicos (las marcas `← entre las comillas…`) y el componente extra si la rúbrica lo pide (sección 9). | Poco |

Para encontrar lo que te falta: **Ctrl+Shift+F `PEGAR ACÁ`** muestra todas las marcas que todavía no pegaste.

**En criollo:** primero hacés que ande (pasos 0 a 3, todo mecánico) y recién después que se vea igual al viejo (paso 4).

---

## 2. Qué da puntos (las 7 rúbricas reparten igual)

| Bloque de la rúbrica | Puntos en los modelos | Lo cubre | Paso |
|---|---|---|---|
| Ruteo, navegación sin recargar, 404 | 20 | `App.jsx`, `NotFound`, los `Link` | 1–2 |
| Pedir datos a la API, cargando / error | 20–25 | `client.js` o `api.js`, `use….js`, `Loading` / `ErrorMessage` | 1–2 |
| Login con Context y localStorage **o** historial con Context y localStorage | 20–25 | `AuthContext`, `useAuth`, `LoginForm` **o** `…RecientesContext`, `use…Recientes`, el detalle | 1–2 |
| Páginas y componentes: mostrar la información, agrupar, filtros, tarjeta | 20 | Home, tarjeta, detalle, filtros **+ el HTML pegado** | 2 y 4 |
| Hooks propios y código limpio | 15 | Los `use….js` ya separados y los nombres de la rúbrica | 2 |

**Desaprobación directa** (en casi todas las rúbricas):
- La app no compila.
- No usa React Router.
- No hay Context / localStorage.
- Usa `innerHTML` o `getElementById`.
- Lee los JSON directo en vez de usar el servidor.

Las plantillas ya evitan todo esto. Lo único que podés romper vos es **la compilación**.

Esto es lo que dicen las rúbricas de práctica: quien corrige es el profe, y el parcial real puede repartir distinto.

**En criollo:** la parte mecánica cubre la mayoría de los bloques. El HTML suma sobre todo en "páginas y componentes".

---

## 3. Cómo elegir familia y versiones

**Familia:** ¿`server/*.js` tiene `app.post('/api/login'` (o el README o la rúbrica hablan de login)? → **LOGIN**. Si no hay login y la rúbrica pide recientes o historial → **HISTORIAL**.

**LOGIN, la línea de OPCIÓN en `HomePage.jsx`:** abrí `http://localhost:PUERTO/api/…` (la ruta de la lista) en el navegador.
- Empieza con `{ "Algo": [` → **A** (ya viene agrupado).
- Empieza con `[` y el JS viejo agrupa con `.filter(x => x.campo === …)` → **B**.
- Empieza con `[` y se muestra todo junto → **C**.

**HISTORIAL, versión de la pantalla de inicio:**
- La pantalla de inicio vieja tiene **un select y un botón** que llevan al detalle → **SIN FILTROS**.
- Tiene **selects y/o buscador y tarjetas** → **CON FILTROS**.

**HISTORIAL, versión de Recientes:**
- La rúbrica dice **"cruzar con la API"**, **"grilla de tarjetas"** o similar → **CRUZAR CON LA API**. Necesita la tarjeta: si elegiste SIN FILTROS, copiá también `__ITEM_CAP__Card.jsx` de CON FILTROS.
- Si no lo dice → **LISTA**.

---

## 4. Fichas de tokens (las completás vos)

### LOGIN (8 tokens)

| Token | De qué archivo | Qué buscar |
|---|---|---|
| `__PUERTO__` | `server/*.js` | la línea `PORT` |
| `__URL__` | `server/*.js` | `app.get('/api/XXX'` de la lista (la que **no** tiene `:id`) → XXX |
| `__RUTA__` | README / rúbrica | la ruta del **navegador** del detalle `/XXX/:id` → XXX |
| `__CLAVE__` | el JS del login (`js/login.js`, `js/auth.js`) | `localStorage.setItem('XXX'` → XXX |
| `__ITEM__` | el JS viejo del **detalle** | `${XXX.algo}` → XXX (la palabra antes del punto) |
| `__ITEM_CAP__` | `rubricas.md` | Ctrl+F `Card` → `XXXCard` → XXX. Si no hay: la cosa en singular con Mayúscula |
| `__LISTA_CAP__` | `rubricas.md` | Ctrl+F `use` → el hook de los datos (`useXXX`, no `useAuth`) → XXX. Si no hay: la cosa en plural con Mayúscula |
| `__CAMPO_GRUPO__` | el JS que pide la lista | `.filter(x => x.XXX === …)` → XXX (**solo OPCIÓN B**; con A o C desaparece solo) |

### HISTORIAL (11 tokens + 5 si hay filtros)

| Token | De qué archivo | Qué buscar |
|---|---|---|
| `__PUERTO__` | `server/*.js` | la línea `PORT` |
| `__URL__` | `server/*.js` | `app.get("/api/XXX"` de la lista → XXX |
| `__WRAP_LISTA__` | `server/*.js` | en el `res.json({ … })` de la lista, el nombre que viene después de `success` y `total`. Si es `res.json(algo)` sin llaves: en `api.js` se borra el punto y la palabra |
| `__WRAP__` | `server/*.js` | el nombre dentro del `res.json({ … })` del detalle. Si es suelto: igual que arriba |
| `__ID_CAMPO__` | `server/*.js` | en el detalle, `.find((x) => x.XXX === req.params…)` → XXX |
| `__NOMBRE__` | `data/*.json` | el campo con el nombre de la cosa. Si está adentro de otro: `a?.b` |
| `__RUTA__` | rúbrica (si no dice, elegido en singular) | la ruta del navegador del detalle |
| `__CLAVE__` | `js/*.js` | `localStorage.getItem("XXX")` → XXX |
| `__ITEM__` | el JS viejo del **detalle** | `${XXX.algo}` → XXX |
| `__ITEM_CAP__` | `rubricas.md` | `XXXCard` → XXX. Si no hay: singular con Mayúscula |
| `__LISTA_CAP__` | `rubricas.md` | `XXXRecientesContext` o `useXXX` → XXX. Si no hay: plural con Mayúscula |
| `__Q1__`, `__Q2__` | `server/README.md` | los `?XXX=` de la lista que usan los **selects**, en el orden en que aparecen los selects en `index.html` |
| `__Q3__` | `server/README.md` | el `?XXX=` del **buscador** de texto |
| `__AUX1__`, `__AUX2__` | `server/*.js` y `js/*.js` | las rutas `/api/XXX` que llenan cada select (las que tienen `fetch` en el JS viejo) |

**Reglas de la ficha:**
- **Una ruta del servidor cuenta solo si el JS viejo tiene un `fetch` que la usa.**
- **`/api/algo` es del servidor** (`__URL__`). **`/algo/:id` es del navegador** (`__RUTA__`). Nunca se mezclan.
- **Si un token no se usa en tu parcial** (no hay 2.º select, no hay buscador), reemplazalo igual por cualquier palabra (ej. `nada2`) y borrá las líneas marcadas `← SELECT 2` / `← BUSCADOR`. Así Ctrl+F `__` da 0.
- **Ctrl+H con "Match case" (Aa) prendido.** Ojo con los tokens pegados a otra palabra: `__LISTA_CAP__RecientesContext` → solo cambia la parte del token.
- **Los nombres de archivo con token también se cambian:** `__ITEM_CAP__Card.jsx` → por ejemplo `GameCard.jsx`.

---

## 5. Las marcas que vas a ver

| Marca | Qué hacés |
|---|---|
| `═══ PEGAR ACÁ: ALGO ═══` + un **provisorio** + `═══ fin provisorio ═══` | Buscás el HTML donde dice **SALE DE**, lo copiás **DESDE / HASTA**, lo traducís (Anexo A) y lo pegás. Después **borrás desde la marca hasta "fin provisorio"**. Si no te da el tiempo, dejalo así: **ya anda**. |
| `═══ PEGAR ACÁ (si hay): ALGO ═══` (sin provisorio) | Si el viejo tiene eso, lo pegás. Si no, borrás el comentario. |
| `{/* ← entre las comillas: … */}` | Un `class` o un texto chico: lo escribís entre las comillas de esa línea y borrás el comentario. Si no te da el tiempo, borrás solo el comentario. |
| `ELEGÍ UNA` + líneas `← OPCIÓN A/B/C` | Dejás la línea de tu opción (sin el comentario) y borrás las otras y la línea `ELEGÍ UNA`. |
| Líneas que terminan en `← SELECT 2` / `← BUSCADOR` | Se borran **solo** si tu parcial no tiene 2.º select o buscador. |

**El provisorio te sirve de ayuda:** muchas veces trae la línea ya traducida que necesitás (el `<Link to=…>`, el `<select value=… onChange=…>`, el `onClick`). Copiala antes de borrarlo.

**En criollo:** `═══` = acá va HTML del viejo; `←` = una cosita chica; lo demás no se toca.

---

## 6. MAPA: cada `PEGAR ACÁ` → de dónde sale

### LOGIN

| Marca (archivo nuevo) | Sale de (archivo viejo) | Qué buscar | Desde → hasta | Ojo al traducir |
|---|---|---|---|---|
| EL HEADER (`Layout.jsx`) | `index.html` | Ctrl+F `<header` | `<header` → `</header>` | el `<form id="loginForm">` y el `<div id="userInfo">` **no** se copian: en su lugar `{areaLogin}` |
| EL SALUDO DEL USUARIO (`Layout.jsx`) | `index.html` (si está vacío: el JS del login) | Ctrl+F `userInfo` (o `Bienvenido`) | `<div id="userInfo"` → su `</div>` | nombre → `{user.fullName}`; botón → `onClick={handleLogout}`; sin `style="display:none"` |
| EL FOOTER, si hay (`Layout.jsx`) | `index.html` | Ctrl+F `<footer` | `<footer` → `</footer>` | — |
| `class` del `<main>` (`Layout.jsx`) | `index.html` | Ctrl+F `<main` | solo el class | — |
| LO FIJO DE ARRIBA, si hay (`HomePage.jsx`) | `index.html` | Ctrl+F `<main` | lo de adentro **antes** del lugar vacío | un título o texto de bienvenida |
| `class` del lugar vacío (`HomePage.jsx`) | `index.html` | el elemento con el loader o "se cargará aquí" | solo el class | sin la palabra `loading` |
| UN GRUPO (`HomePage.jsx`) | el JS que pide la lista | Ctrl+F `<h2` | el HTML de **un** grupo | `${grupo}` → `{grupo}`; donde iban las tarjetas → `{tarjetas}` |
| LO DE ARRIBA DEL HTML (`…Card.jsx`) | el JS que pide la lista | la función que arma la tarjeta | de su `{` hasta antes del `return` | si el elemento se llama distinto, cambiarlo por `__ITEM__` |
| LA TARJETA (`…Card.jsx`) | el JS que pide la lista (`fetch` a `/api/__URL__`) | Ctrl+F `card` | adentro del backtick `` ` `` | `<a href="algo.html?id=${id}">` → `<Link to={…}>` (copiá el del provisorio) |
| LO DE ARRIBA DEL HTML (`…DetailPage.jsx`) | el JS del detalle | los `const` antes del `innerHTML =` | — | si hace falta un dato de la lista: está en `lista` |
| EL DETALLE (`…DetailPage.jsx`) | **1)** el `.html` del detalle **2)** el JS del detalle | **1)** `<main` **2)** `innerHTML = \`` (el más largo) | **1)** `<main` → `</main>` **2)** adentro del backtick | **1)** `<main>` → `<div>`. **2)** va adentro del lugar vacío de 1 |

### HISTORIAL

| Marca (archivo nuevo) | Sale de (archivo viejo) | Qué buscar | Desde → hasta | Ojo al traducir |
|---|---|---|---|---|
| EL HEADER (`Header.jsx`) | `index.html` | Ctrl+F `<header` | `<header` → `</header>` | botones de navegación → `NavLink` (copiá los del provisorio). **Si no hay `<header>`: dejá el provisorio** |
| EL FOOTER, si hay (`App.jsx`) | `index.html` | Ctrl+F `<footer` | `<footer` → `</footer>` | — |
| `class` del `<main>` (`App.jsx`) | `index.html` | Ctrl+F `<main` | solo el class | — |
| LA PANTALLA DE INICIO (`Home.jsx` **sin filtros**) | `index.html` | el `<body>` (o la `<section>` de inicio) | lo de adentro, sin `<script>` (la `<section>` no va) | form → `onSubmit={consultar}`; select → el del provisorio; `<ul>` vacío → `{itemsRecientes}` |
| `class` de la grilla y textos (`Home.jsx` **con filtros**) | `index.html` y el JS | Ctrl+F `grid`, `empty-message` | solo el class / el texto | — |
| textos de los filtros (`Filtros.jsx`) | `index.html` | Ctrl+F `<select` | la 1.ª `<option>` y el `placeholder` | opcional |
| LO DE ARRIBA DEL HTML (`…Card.jsx`) | el JS que pide la lista | la función que arma la tarjeta | de su `{` hasta antes del `return` | si el elemento se llama distinto, cambiarlo por `__ITEM__` |
| LA TARJETA (`…Card.jsx`) | el JS que pide la lista | Ctrl+F `card` | adentro del backtick | el `<div onclick>` de afuera → `<Link to={…} className="…">` |
| LA PANTALLA DE RECIENTES (`Recientes.jsx` **lista**) | `index.html` o la pantalla vieja con el historial | Ctrl+F `historial` | del título al último botón | `<ul>` vacío → `{itemsRecientes}`; limpiar → `onClick={limpiarRecientes}` |
| título, vacío y grilla (`Recientes.jsx` **cruzar**) | `index.html` | la `<section>` de recientes | solo textos / class | — |
| LO DE ARRIBA DEL HTML (`…Detail.jsx`) | el JS del detalle | los `const` antes del `innerHTML =` | — | — |
| EL DETALLE (`…Detail.jsx`) | **1)** la pantalla de detalle (otro `.html` o la `<section>` de detalle) **2)** el JS del detalle | **2)** `innerHTML = \`` (el más largo) | **1)** lo de adentro **2)** adentro del backtick | Volver → `onClick={() => navigate("/")}`; filas `<tr>` → dentro de `<tbody>` |

**Seguir el hilo (cuando lo pegado usa `${algo}` que no es un campo):** Ctrl+F `algo` en el mismo JS.
- Si es `const algo = …` o `function algo(…)` → va en **LO DE ARRIBA DEL HTML**.
- Si es `const algoHtml = lista.map(…)` con HTML adentro → se traduce y va **donde estaba `${algoHtml}`**, como `{lista.map((x, i) => <li key={i}>…</li>)}`.

**Lo que NO se copia nunca** (React ya lo hace solo):
- `document.getElementById`, `querySelector`
- `addEventListener`, `classList`, `.style.display`
- `container.innerHTML =` (la línea; el HTML de adentro sí)
- `window.location`

**En criollo:** el header y el footer salen del `index.html`; la tarjeta y el grupo salen del JS de la lista; el detalle sale del `.html` del detalle más el `innerHTML` más largo de su JS.


---

## 7. PLANTILLA LOGIN (en el orden en que se hacen)

#### L1. `react/src/hooks/useAuth.js`

```js
// PASO 1 · COPIAR TAL CUAL (si la rúbrica lo llama distinto, ej. useLogin, renombralo al final si sobra tiempo)
import { useContext } from "react";
import { AuthContext } from "../context/AuthContext.jsx";

export function useAuth() {
  const ctx = useContext(AuthContext);

  if (!ctx) {
    throw new Error("useAuth debe usarse dentro de un <AuthProvider>");
  }

  return ctx;
}
```

#### L2. `react/src/components/LoginForm.jsx`

```jsx
// PASO 1 · COPIAR TAL CUAL
import { useState } from "react";
import { useAuth } from "../hooks/useAuth.js";
import { apiFetch } from "../api/client.js";

export function LoginForm() {
  const { login } = useAuth();
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(false);

  const handleSubmit = async (event) => {
    event.preventDefault();
    setError(null);
    setLoading(true);
    try {
      const datos = await apiFetch("/login", {
        method: "POST",
        body: JSON.stringify({ username, password }),
      });
      login({
        fullName: datos.firstName
          ? `${datos.firstName} ${datos.lastName}`
          : datos.username,
        rol: datos.rol || "",
      });
    } catch (e) {
      setError(e);
    } finally {
      setLoading(false);
    }
  };

  return (
    <form id="loginForm" onSubmit={handleSubmit}>
      <input
        type="text"
        id="username"
        placeholder="Usuario"
        value={username}
        onChange={(e) => setUsername(e.target.value)}
        required
      />
      <input
        type="password"
        id="password"
        placeholder="Contraseña"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        required
      />
      <button type="submit" disabled={loading}>
        {loading ? "Ingresando..." : "Ingresar"}
      </button>
      {error && (
        <p id="loginError" className="login-error">
          {error.message}
        </p>
      )}
    </form>
  );
}
```

#### L3. `react/src/components/VerDatos.jsx`

```jsx
// PASO 1 · COPIAR TAL CUAL
// Muestra los datos tal como vienen del servidor. Lo usan las partes PROVISORIAS:
// así la app ya anda (y se ve algo) antes de pegar el HTML del parcial.
export function VerDatos({ dato, corto = false }) {
  if (!dato) return null;
  let filas = Object.entries(dato).filter(([, valor]) => valor !== null && valor !== undefined);
  if (corto) filas = filas.filter(([, valor]) => typeof valor !== "object").slice(0, 3);
  return (
    <div style={{ background: "#fff", color: "#222", padding: "8px", margin: "8px 0" }}>
      {filas.map(([campo, valor]) => (
        <p key={campo}>
          <strong>{campo}:</strong> {typeof valor === "object" ? JSON.stringify(valor) : String(valor)}
        </p>
      ))}
    </div>
  );
}

export default VerDatos;
```

#### L4. `react/src/pages/NotFoundPage.jsx`

```jsx
// PASO 1 · COPIAR TAL CUAL
import { Link } from "react-router-dom";

export function NotFoundPage() {
  return (
    <div className="error">
      <h1>404</h1>
      <p>La página que buscás no existe.</p>
      <Link to="/">Volver al inicio</Link>
    </div>
  );
}
```

#### L5. `react/src/components/Layout.jsx`

```jsx
// PASO 1 · COPIAR (ya anda con lo provisorio)  ·  PASO 4 · PEGAR HTML (header, saludo, footer)
import { Link, useNavigate } from "react-router-dom";
import { useAuth } from "../hooks/useAuth.js";
import { LoginForm } from "./LoginForm.jsx";

export function Layout({ children }) {
  const { user, logout } = useAuth();
  const navigate = useNavigate();

  const handleLogout = () => {
    logout();
    navigate("/");
  };

  // Si hay usuario se ve el saludo; si no, el formulario de login (ya está hecho, no se toca)
  const areaLogin = user ? (
    <>
      {/* ═══ PEGAR ACÁ: EL SALUDO DEL USUARIO ═══
          SALE DE: index.html → Ctrl+F userInfo → desde <div id="userInfo" hasta su </div>
                   (si en el index.html ese lugar está vacío: el JS del login → Ctrl+F Bienvenido)
          AL TRADUCIR: el nombre → {user.fullName} · el rol (si se muestra) → {user.rol}
                       el botón de salir lleva onClick={handleLogout} · borrá style="display: none"
                       si tiene un class que lo esconde (…-hidden), poné el que usa el JS para mostrarlo
                       (en el JS del login, Ctrl+F userInfo.classList)
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <div id="userInfo">
        <span>Bienvenido, {user.fullName}</span>
        <button id="logoutBtn" onClick={handleLogout}>
          Cerrar sesión
        </button>
      </div>
      {/* ═══ fin provisorio ═══ */}
    </>
  ) : (
    <LoginForm />
  );

  return (
    <>
      {/* ═══ PEGAR ACÁ: EL HEADER ═══
          SALE DE: index.html → Ctrl+F <header → desde <header hasta </header>
          AL TRADUCIR: el <form id="loginForm"> y el <div id="userInfo"> NO se copian: en su lugar
                       escribí {areaLogin} (una sola vez). Si el lugar del login está vacío (lo llena el JS),
                       escribí {areaLogin} adentro. Un <a href="index.html"> pasa a <Link to="/">
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <header>
        <Link to="/">Inicio</Link>
        {areaLogin}
      </header>
      {/* ═══ fin provisorio ═══ */}

      <main className="">{/* ← entre las comillas: el class del <main> del index.html (Ctrl+F <main). Si no tiene, dejalo así */}
        {children}
      </main>

      {/* ═══ PEGAR ACÁ (si hay): EL FOOTER ═══
          SALE DE: index.html → Ctrl+F <footer → desde <footer hasta </footer>
          Si no hay footer, borrá esta marca */}
    </>
  );
}
```

#### L6. `react/src/api/client.js`

```js
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)
export const API_BASE_URL = "http://localhost:__PUERTO__/api";

export async function apiFetch(path, options = {}) {
  const response = await fetch(`${API_BASE_URL}${path}`, {
    headers: { "Content-Type": "application/json" },
    ...options,
  });
  const datos = await response.json().catch(() => null);
  if (!response.ok) {
    throw new Error(datos?.error || "Error al conectar con el servidor");
  }
  return datos;
}
```

#### L7. `react/src/context/AuthContext.jsx`

```jsx
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)
import { createContext, useState, useEffect } from "react";

export const AuthContext = createContext(null);

const CLAVE = "__CLAVE__";

export function AuthProvider({ children }) {
  const [user, setUser] = useState(() => {
    const guardado = localStorage.getItem(CLAVE);
    return guardado ? JSON.parse(guardado) : null;
  });

  useEffect(() => {
    if (user) {
      localStorage.setItem(CLAVE, JSON.stringify(user));
    } else {
      localStorage.removeItem(CLAVE);
    }
  }, [user]);

  const login = (userData) => setUser(userData);
  const logout = () => setUser(null);

  const value = { user, login, logout };

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}
```

#### L8. `react/src/hooks/use__LISTA_CAP__.js`

```js
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)
import { useEffect, useState } from "react";
import { apiFetch } from "../api/client.js";

export function use__LISTA_CAP__() {
  const [datos, setDatos] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function cargar() {
      try {
        setLoading(true);
        setError(null);
        const respuesta = await apiFetch("/__URL__");
        setDatos(respuesta);
      } catch (e) {
        setError(e);
      } finally {
        setLoading(false);
      }
    }
    cargar();
  }, []);

  return { datos, loading, error };
}
```

#### L9. `react/src/App.jsx`

```jsx
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { AuthProvider } from "./context/AuthContext.jsx";
import { Layout } from "./components/Layout.jsx";
import { HomePage } from "./pages/HomePage.jsx";
import { __ITEM_CAP__DetailPage } from "./pages/__ITEM_CAP__DetailPage.jsx";
import { NotFoundPage } from "./pages/NotFoundPage.jsx";

export default function App() {
  return (
    <BrowserRouter>
      <AuthProvider>
        <Layout>
          <Routes>
            <Route path="/" element={<HomePage />} />
            <Route path="/__RUTA__/:id" element={<__ITEM_CAP__DetailPage />} />
            <Route path="*" element={<NotFoundPage />} />
          </Routes>
        </Layout>
      </AuthProvider>
    </BrowserRouter>
  );
}
```

#### L10. `react/src/pages/HomePage.jsx`

```jsx
// PASO 2 · REEMPLAZAR + ELEGIR UNA OPCIÓN  ·  PASO 4 · PEGAR HTML (un grupo)
import { Fragment } from "react";
import { use__LISTA_CAP__ } from "../hooks/use__LISTA_CAP__.js";
import { __ITEM_CAP__Card } from "../components/__ITEM_CAP__Card.jsx";

// No se toca: arma los grupos cuando el servidor manda una lista sin agrupar
function agrupar(lista, campo) {
  const nombres = [...new Set(lista.map((x) => x[campo]))].sort();
  return nombres.map((nombre) => [nombre, lista.filter((x) => x[campo] === nombre)]);
}

export function HomePage() {
  const { datos, loading, error } = use__LISTA_CAP__();

  if (loading) {
    return (
      <article className="container loading">
        <div className="loader"></div>
      </article>
    );
  }

  if (error) {
    return (
      <div className="error">
        <h1>Error al cargar los datos</h1>
        <p>{error.message}</p>
      </div>
    );
  }

  // ELEGÍ UNA de estas 3 líneas y borrá las otras 2 (abrí http://localhost:PUERTO/api/... en el navegador y mirá):
  const grupos = Object.entries(datos || {}); // ← OPCIÓN A: empieza con { "Grupo1": [ ... ], "Grupo2": [ ... ] }
  const grupos = agrupar(datos || [], "__CAMPO_GRUPO__"); // ← OPCIÓN B: empieza con [ y el JS viejo agrupa con .filter
  const grupos = [["", datos || []]]; // ← OPCIÓN C: empieza con [ y el JS viejo muestra todo junto, sin grupos

  const conDatos = grupos.filter(([, items]) => items.length > 0);

  if (conDatos.length === 0) {
    return (
      <div className="error">
        <p>No hay datos para mostrar.</p>
      </div>
    );
  }

  return (
    <>
      {/* ═══ PEGAR ACÁ (si hay): LO FIJO DE ARRIBA DE LA HOME ═══
          SALE DE: index.html → Ctrl+F <main → lo que está adentro del <main> ANTES del lugar vacío
                   donde el JS mete las tarjetas (un título grande, un texto de bienvenida)
          Si no hay nada, borrá esta marca */}
      <div className="">{/* ← entre las comillas: el class del lugar vacío donde el JS mete todo (index.html: el que tiene el loader o el comentario "se cargará aquí"). Si dice "loading", esa palabra no va */}
        {conDatos.map(([grupo, items]) => {
          const tarjetas = items.map((x) => (
            <__ITEM_CAP__Card key={x.id} __ITEM__={x} grupo={grupo} />
          ));
          return (
            <Fragment key={grupo}>
              {/* ═══ PEGAR ACÁ: UN GRUPO ═══
                  SALE DE: el JS que pide la lista → Ctrl+F <h2 → el HTML que arma UN grupo
                           (su título y, si tiene, el <div> donde van las tarjetas)
                  AL TRADUCIR: el nombre del grupo (${lo que sea}) → {grupo}
                               el lugar donde iban las tarjetas → {tarjetas}
                               si las tarjetas no van adentro del grupo sino después, poné {tarjetas} después
                  SI ELEGISTE OPCIÓN C (sin grupos): pegá solo el <div> que envuelve las tarjetas, con {tarjetas} adentro
                  Al pegar, borrá desde esta marca hasta "fin provisorio" */}
              <section>
                <h2>{grupo}</h2>
                <div>{tarjetas}</div>
              </section>
              {/* ═══ fin provisorio ═══ */}
            </Fragment>
          );
        })}
      </div>
    </>
  );
}
```

#### L11. `react/src/components/__ITEM_CAP__Card.jsx`

```jsx
// PASO 2 · REEMPLAZAR (ya anda con lo provisorio)  ·  PASO 4 · PEGAR HTML (la tarjeta)
import { Link } from "react-router-dom";
import { VerDatos } from "./VerDatos.jsx";

export function __ITEM_CAP__Card({ __ITEM__, grupo }) {
  /* ═══ PEGAR ACÁ (si hay): LO DE ARRIBA DEL HTML ═══
     SALE DE: el mismo JS de donde sacás la tarjeta → la función que la arma
              → desde la línea siguiente a su { de apertura hasta la línea anterior al return
              (líneas como const { id, nombre } = algo  o  const algo = ...)
     Si "algo" no se llama __ITEM__, cambiá esa palabra por __ITEM__.
     Si la función recibía un 2.º dato (el nombre del grupo), acá ese dato se llama grupo.
     Si el HTML usa una función que no copiaste (la consola dice "... is not defined"):
     buscala en el mismo JS y copiala entera acá también.
     Si no hay nada, borrá este comentario */

  return (
    <>
      {/* ═══ PEGAR ACÁ: LA TARJETA ═══
          SALE DE: el JS que pide la lista (el que tiene fetch a /api/__URL__) → Ctrl+F card
                   → la función o el .map que devuelve el HTML de UNA tarjeta
          DESDE: lo que sigue al ` de apertura   HASTA: lo anterior al ` de cierre
          AL TRADUCIR: <a href="algo.html?id=${id}"> → <Link to={`/__RUTA__/${__ITEM__.id}`}> y su </a> → </Link>
                       (si no hay <a> y el <div> de afuera tiene onclick, ese <div> pasa a ser el <Link>)
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <Link to={`/__RUTA__/${__ITEM__.id}`}>
        <VerDatos dato={__ITEM__} corto />
      </Link>
      {/* ═══ fin provisorio ═══ */}
    </>
  );
}
```

#### L12. `react/src/pages/__ITEM_CAP__DetailPage.jsx`

```jsx
// PASO 2 · REEMPLAZAR  ·  PASO 4 · PEGAR HTML (el detalle)
import { useParams, Link } from "react-router-dom";
import { useState, useEffect } from "react";
import { apiFetch } from "../api/client.js";
import { VerDatos } from "../components/VerDatos.jsx";

export function __ITEM_CAP__DetailPage() {
  const { id } = useParams();
  const [__ITEM__, set__ITEM_CAP__] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  // No se toca: también trae la lista completa, por si el detalle muestra un dato que solo está ahí
  const [lista, setLista] = useState(null);
  useEffect(() => {
    apiFetch("/__URL__")
      .then(setLista)
      .catch(() => setLista(null));
  }, []);

  useEffect(() => {
    async function cargar() {
      try {
        setLoading(true);
        setError(null);
        const datos = await apiFetch(`/__URL__/${id}`);
        set__ITEM_CAP__(datos);
      } catch (e) {
        setError(e);
      } finally {
        setLoading(false);
      }
    }
    cargar();
  }, [id]);

  if (loading) {
    return (
      <article className="container loading">
        <div className="loader"></div>
      </article>
    );
  }

  if (error || !__ITEM__) {
    return (
      <article className="container">
        <p className="error">{error ? error.message : "No encontrado"}</p>
        <Link to="/">Volver al inicio</Link>
      </article>
    );
  }

  /* ═══ PEGAR ACÁ (si hay): LO DE ARRIBA DEL HTML ═══
     SALE DE: el JS del detalle → las líneas const que están antes del innerHTML = `
              (listas armadas con .map, cálculos) y las funciones que el HTML usa
     Si el elemento se llama distinto de __ITEM__ en esas líneas, cambiá esa palabra por __ITEM__.
     Si el JS viejo pedía también la lista, acá la tenés en "lista" (puede estar vacía al principio: lista && ...)
     Si no hay nada, borrá este comentario */

  return (
    <>
      {/* ═══ PEGAR ACÁ: EL DETALLE ═══  (son dos pedazos, uno adentro del otro)
          1) SALE DE: el .html de la página de detalle (el que no es index.html) → Ctrl+F <main
             DESDE: <main   HASTA: </main>
             AL TRADUCIR: <main …> pasa a <div …> y </main> a </div> (el <main> ya está en el Layout)
                          <a href="index.html" …> pasa a <Link to="/" …>
          2) SALE DE: el JS del detalle (el que tiene fetch a /api/__URL__/${id}) → Ctrl+F innerHTML = `
                      → el más largo (el que se usa cuando todo salió bien)
             DESDE: lo que sigue al ` de apertura   HASTA: lo anterior al ` de cierre
             VA: adentro del lugar vacío del pedazo 1 (donde el JS metía el detalle; si tiene un loader, borralo)
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <div style={{ background: "#fff", color: "#222", padding: "1rem" }}>
        <VerDatos dato={__ITEM__} />
        <Link to="/">Volver</Link>
      </div>
      {/* ═══ fin provisorio ═══ */}
    </>
  );
}
```


---

## 8. PLANTILLA HISTORIAL (en el orden en que se hacen)

Cada archivo dice de qué carpeta es: **SIEMPRE** (va en todos los parciales de esta familia), **SIN FILTROS** o **CON FILTROS** (elegís una de las dos según la pantalla de inicio) y **RECIENTES · LISTA** o **RECIENTES · CRUZAR CON LA API** (elegís una).

#### H1. `react/src/components/Loading.jsx`  ·  SIEMPRE

```jsx
// PASO 1 · COPIAR TAL CUAL
function Loading() {
  return <div className="loading">Cargando...</div>;
}

export default Loading;
```

#### H2. `react/src/components/ErrorMessage.jsx`  ·  SIEMPRE

```jsx
// PASO 1 · COPIAR TAL CUAL
function ErrorMessage({ message }) {
  return <div className="error-message">{message}</div>;
}

export default ErrorMessage;
```

#### H3. `react/src/pages/NotFound.jsx`  ·  SIEMPRE

```jsx
// PASO 1 · COPIAR TAL CUAL
import { Link } from "react-router-dom";

function NotFound() {
  return (
    <div className="not-found">
      <div className="container">
        <h2>404</h2>
        <p>La página que buscás no existe.</p>
        <Link to="/">Volver al inicio</Link>
      </div>
    </div>
  );
}

export default NotFound;
```

#### H4. `react/src/components/VerDatos.jsx`  ·  SIEMPRE

```jsx
// PASO 1 · COPIAR TAL CUAL
// Muestra los datos tal como vienen del servidor. Lo usan las partes PROVISORIAS:
// así la app ya anda (y se ve algo) antes de pegar el HTML del parcial.
export function VerDatos({ dato, corto = false }) {
  if (!dato) return null;
  let filas = Object.entries(dato).filter(([, valor]) => valor !== null && valor !== undefined);
  if (corto) filas = filas.filter(([, valor]) => typeof valor !== "object").slice(0, 3);
  return (
    <div style={{ background: "#fff", color: "#222", padding: "8px", margin: "8px 0" }}>
      {filas.map(([campo, valor]) => (
        <p key={campo}>
          <strong>{campo}:</strong> {typeof valor === "object" ? JSON.stringify(valor) : String(valor)}
        </p>
      ))}
    </div>
  );
}

export default VerDatos;
```

#### H5. `react/src/components/Header.jsx`  ·  SIEMPRE

```jsx
// PASO 1 · COPIAR (ya anda con lo provisorio)  ·  PASO 4 · PEGAR HTML (el header)
import { NavLink } from "react-router-dom";

function Header() {
  return (
    <>
      {/* ═══ PEGAR ACÁ: EL HEADER ═══
          SALE DE: index.html → Ctrl+F <header → desde <header hasta </header>
                   (si el index.html NO tiene <header>, dejá el provisorio como está y borrá solo esta marca)
          AL TRADUCIR: cada botón o link que cambia de pantalla (Inicio, Recientes…) pasa a ser un NavLink
                       como los de abajo, con el mismo class que tenía el botón:
                       <NavLink to="/" end className="…">Inicio</NavLink>   <NavLink to="/recientes" className="…">Recientes</NavLink>
                       (borrá los atributos data-… que usaba el JS y la palabra active: NavLink la pone solo)
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <header>
        <nav>
          <NavLink to="/" end>
            Inicio
          </NavLink>{" "}
          <NavLink to="/recientes">Recientes</NavLink>
        </nav>
      </header>
      {/* ═══ fin provisorio ═══ */}
    </>
  );
}

export default Header;
```

#### H6. `react/src/context/__LISTA_CAP__RecientesContext.jsx`  ·  SIEMPRE

```jsx
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)
import { createContext, useState, useEffect } from "react";

export const __LISTA_CAP__RecientesContext = createContext();

export function __LISTA_CAP__RecientesProvider({ children }) {
  const CLAVE = "__CLAVE__";
  const TOPE = 15;

  const [recientes, setRecientes] = useState(() => {
    const guardado = localStorage.getItem(CLAVE);
    return guardado ? JSON.parse(guardado) : [];
  });

  useEffect(() => {
    localStorage.setItem(CLAVE, JSON.stringify(recientes));
  }, [recientes]);

  const agregarReciente = (id, nombre) => {
    setRecientes((prev) => {
      const sinRepetir = prev.filter((r) => r.id !== id);
      const nuevo = { id, nombre, fecha: new Date().toLocaleString() };
      return [nuevo, ...sinRepetir].slice(0, TOPE);
    });
  };

  const limpiarRecientes = () => setRecientes([]);

  return (
    <__LISTA_CAP__RecientesContext.Provider
      value={{ recientes, agregarReciente, limpiarRecientes }}
    >
      {children}
    </__LISTA_CAP__RecientesContext.Provider>
  );
}
```

#### H7. `react/src/hooks/use__LISTA_CAP__Recientes.js`  ·  SIEMPRE

```js
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)
import { useContext } from "react";
import { __LISTA_CAP__RecientesContext } from "../context/__LISTA_CAP__RecientesContext";

export function use__LISTA_CAP__Recientes() {
  const context = useContext(__LISTA_CAP__RecientesContext);

  if (!context) {
    throw new Error(
      "use__LISTA_CAP__Recientes debe usarse dentro de __LISTA_CAP__RecientesProvider"
    );
  }

  return context;
}
```

#### H8. `react/src/App.jsx`  ·  SIEMPRE

```jsx
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)  ·  PASO 4 · PEGAR HTML (footer, si hay)
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { __LISTA_CAP__RecientesProvider } from "./context/__LISTA_CAP__RecientesContext";
import Header from "./components/Header";
import Home from "./pages/Home";
import __ITEM_CAP__Detail from "./pages/__ITEM_CAP__Detail";
import Recientes from "./pages/Recientes";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <__LISTA_CAP__RecientesProvider>
      <BrowserRouter>
        <Header />
        <main className="">{/* ← entre las comillas: el class del <main> del index.html (Ctrl+F <main). Si no tiene, dejalo así */}
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/__RUTA__/:id" element={<__ITEM_CAP__Detail />} />
            <Route path="/recientes" element={<Recientes />} />
            <Route path="*" element={<NotFound />} />
          </Routes>
        </main>
        {/* ═══ PEGAR ACÁ (si hay): EL FOOTER ═══
            SALE DE: index.html → Ctrl+F <footer → desde <footer hasta </footer>
            Si no hay footer, borrá esta marca */}
      </BrowserRouter>
    </__LISTA_CAP__RecientesProvider>
  );
}

export default App;
```

#### H9. `react/src/pages/__ITEM_CAP__Detail.jsx`  ·  SIEMPRE

```jsx
// PASO 2 · REEMPLAZAR  ·  PASO 4 · PEGAR HTML (el detalle)
import { useState, useEffect } from "react";
import { useParams, useNavigate, Link } from "react-router-dom";
import Loading from "../components/Loading";
import ErrorMessage from "../components/ErrorMessage";
import VerDatos from "../components/VerDatos";
import { get__ITEM_CAP__ } from "../services/api";
import { use__LISTA_CAP__Recientes } from "../hooks/use__LISTA_CAP__Recientes";

function __ITEM_CAP__Detail() {
  const { id } = useParams();
  const navigate = useNavigate();
  const { recientes, agregarReciente, limpiarRecientes } = use__LISTA_CAP__Recientes();

  const [__ITEM__, set__ITEM_CAP__] = useState(null);
  const [cargando, setCargando] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function cargar() {
      try {
        setCargando(true);
        setError(null);
        const datos = await get__ITEM_CAP__(id);
        set__ITEM_CAP__(datos);
        agregarReciente(id, datos.__NOMBRE__);
      } catch (e) {
        setError("No encontrado");
      } finally {
        setCargando(false);
      }
    }
    cargar();
  }, [id]);

  if (cargando) return <Loading />;
  if (error) return <ErrorMessage message={error} />;
  if (!__ITEM__) return null;

  // Listo para usar si el detalle viejo muestra el historial: escribí {itemsRecientes} adentro de su <ul>
  const itemsRecientes = recientes.map((r) => (
    <li key={r.id}>
      <Link to={`/__RUTA__/${r.id}`}>
        {r.nombre} - {r.fecha}
      </Link>
    </li>
  ));

  /* ═══ PEGAR ACÁ (si hay): LO DE ARRIBA DEL HTML ═══
     SALE DE: el JS del detalle → las líneas const que están antes del innerHTML = `
              (listas armadas con .map, cálculos) y las funciones que el HTML usa
     Si el elemento se llama distinto de __ITEM__ en esas líneas, cambiá esa palabra por __ITEM__.
     Si no hay nada, borrá este comentario */

  return (
    <>
      {/* ═══ PEGAR ACÁ: EL DETALLE ═══  (son dos pedazos, uno adentro del otro)
          1) SALE DE: la pantalla de detalle vieja:
                      - si es otro .html: lo de adentro de su <body> (sin los <script>)
                      - si está en index.html: Ctrl+F detalle → lo de ADENTRO de esa <section> (la etiqueta <section> no va)
             AL TRADUCIR: botón Volver → onClick={() => navigate("/")}
                          botón de limpiar el historial → onClick={limpiarRecientes}
                          el <ul> vacío del historial → <ul>{itemsRecientes}</ul>
                          si el <h1> ya está en el Header, no lo repitas
          2) SALE DE: el JS del detalle (el que tiene fetch a /api/__URL__/${id}) → Ctrl+F innerHTML = `
                      → el más largo (el que se usa cuando todo salió bien)
             DESDE: lo que sigue al ` de apertura   HASTA: lo anterior al ` de cierre
             VA: adentro del lugar vacío del pedazo 1 (donde el JS metía el detalle)
                 si son filas <tr>: adentro de <tbody> … </tbody> dentro de la <table>
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <div className="container">
        <button onClick={() => navigate("/")}>← Volver</button>
        <h2>{__ITEM__.__NOMBRE__}</h2>
        <VerDatos dato={__ITEM__} />
      </div>
      {/* ═══ fin provisorio ═══ */}
    </>
  );
}

export default __ITEM_CAP__Detail;
```

#### H10. `react/src/services/api.js`  ·  SIN FILTROS

```js
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)  ·  versión SIN FILTROS
const API_BASE = "http://localhost:__PUERTO__/api";

export async function get__LISTA_CAP__() {
  try {
    const response = await fetch(`${API_BASE}/__URL__`);
    if (!response.ok) throw new Error("Error al cargar");
    const datos = await response.json();
    return datos.__WRAP_LISTA__; // ← si el servidor responde res.json(algo) sin nombre adentro: borrá el punto y la palabra (queda: return datos;)
  } catch (error) {
    console.error("Error al cargar la lista:", error);
    throw error;
  }
}

export async function get__ITEM_CAP__(id) {
  try {
    const response = await fetch(`${API_BASE}/__URL__/${id}`);
    if (!response.ok) throw new Error("No encontrado");
    const datos = await response.json();
    return datos.__WRAP__; // ← si el servidor responde res.json(algo) sin nombre adentro: borrá el punto y la palabra (queda: return datos;)
  } catch (error) {
    console.error("Error al cargar el elemento:", error);
    throw error;
  }
}
```

#### H11. `react/src/hooks/use__LISTA_CAP__.js`  ·  SIN FILTROS

```js
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)  ·  versión SIN FILTROS
import { useState, useEffect } from "react";
import { get__LISTA_CAP__ } from "../services/api";

export function use__LISTA_CAP__() {
  const [lista, setLista] = useState([]);
  const [cargando, setCargando] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function cargar() {
      try {
        setCargando(true);
        setError(null);
        const datos = await get__LISTA_CAP__();
        setLista(datos);
      } catch (e) {
        setError("No pudimos cargar los datos");
      } finally {
        setCargando(false);
      }
    }
    cargar();
  }, []);

  return { lista, cargando, error };
}
```

#### H12. `react/src/pages/Home.jsx`  ·  SIN FILTROS

```jsx
// PASO 2 · REEMPLAZAR  ·  PASO 4 · PEGAR HTML (la pantalla de inicio)  ·  versión SIN FILTROS (un select y un botón)
import { useState, useEffect } from "react";
import { useNavigate, Link } from "react-router-dom";
import Loading from "../components/Loading";
import ErrorMessage from "../components/ErrorMessage";
import { use__LISTA_CAP__ } from "../hooks/use__LISTA_CAP__";
import { use__LISTA_CAP__Recientes } from "../hooks/use__LISTA_CAP__Recientes";

function Home() {
  const navigate = useNavigate();
  const { recientes } = use__LISTA_CAP__Recientes();
  const { lista, cargando, error } = use__LISTA_CAP__();
  const [seleccionado, setSeleccionado] = useState("");

  // No se toca: si no hay nada elegido, queda elegido el primero
  useEffect(() => {
    if (!seleccionado && lista.length > 0) {
      setSeleccionado(lista[0].__NOMBRE__);
    }
  }, [lista]);

  const consultar = (e) => {
    e.preventDefault();
    const elegido = lista.find((x) => x.__NOMBRE__ === seleccionado);
    if (elegido) navigate(`/__RUTA__/${elegido.__ID_CAMPO__}`);
  };

  const opciones = lista.map((x) => (
    <option key={`${x.__ID_CAMPO__}-${x.__NOMBRE__}`} value={x.__NOMBRE__}>
      {x.__NOMBRE__}
    </option>
  ));

  const itemsRecientes = recientes.map((r) => (
    <li key={r.id}>
      <Link to={`/__RUTA__/${r.id}`}>
        {r.nombre} - {r.fecha}
      </Link>
    </li>
  ));

  if (cargando) return <Loading />;
  if (error) return <ErrorMessage message={error} />;

  return (
    <>
      {/* ═══ PEGAR ACÁ: LA PANTALLA DE INICIO ═══
          SALE DE: index.html → lo de adentro del <body> (sin los <script>)
                   (si el index.html tiene varias <section>, una por pantalla: lo de ADENTRO de la de inicio)
          AL TRADUCIR (las piezas ya traducidas están en el provisorio de abajo: copialas antes de borrarlo):
                       <form …> → <form onSubmit={consultar} …>
                       el <select> vacío → <select value={seleccionado} onChange={(e) => setSeleccionado(e.target.value)}>{opciones}</select>
                       el <ul> vacío del historial → <ul>{itemsRecientes}</ul>
                       el botón que mostraba el historial → <Link to="/recientes" className="…">…</Link>
                       un <a href="otra.html"> a otra pantalla → borralo (o <Link to="/…">)
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <div className="container">
        <form onSubmit={consultar}>
          <select value={seleccionado} onChange={(e) => setSeleccionado(e.target.value)}>
            {opciones}
          </select>
          <button type="submit">Consultar</button>
        </form>
        <ul>{itemsRecientes}</ul>
        <Link to="/recientes">Ver recientes</Link>
      </div>
      {/* ═══ fin provisorio ═══ */}
    </>
  );
}

export default Home;
```

#### H13. `react/src/services/api.js`  ·  CON FILTROS

```js
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)  ·  versión CON FILTROS
// Si hay un solo select: borrá las líneas que terminan en "← SELECT 2" (la función getOpciones2 dejala, no molesta).
// Si no hay buscador de texto: borrá las líneas que terminan en "← BUSCADOR".
const API_BASE = "http://localhost:__PUERTO__/api";

export async function get__LISTA_CAP__(filtros = {}) {
  try {
    const params = new URLSearchParams();
    if (filtros.__Q1__) params.append("__Q1__", filtros.__Q1__);
    if (filtros.__Q2__) params.append("__Q2__", filtros.__Q2__); // ← SELECT 2
    if (filtros.__Q3__) params.append("__Q3__", filtros.__Q3__); // ← BUSCADOR

    const response = await fetch(`${API_BASE}/__URL__?${params}`);
    if (!response.ok) throw new Error("Error al cargar");
    const datos = await response.json();
    return datos.__WRAP_LISTA__; // ← si el servidor responde res.json(algo) sin nombre adentro: borrá el punto y la palabra (queda: return datos;)
  } catch (error) {
    console.error("Error al cargar la lista:", error);
    throw error;
  }
}

export async function get__ITEM_CAP__(id) {
  try {
    const response = await fetch(`${API_BASE}/__URL__/${id}`);
    if (!response.ok) throw new Error("No encontrado");
    const datos = await response.json();
    return datos.__WRAP__; // ← si el servidor responde res.json(algo) sin nombre adentro: borrá el punto y la palabra (queda: return datos;)
  } catch (error) {
    console.error("Error al cargar el elemento:", error);
    throw error;
  }
}

// Las opciones de cada select (cada una sale de su propia ruta del servidor)
export async function getOpciones1() {
  const response = await fetch(`${API_BASE}/__AUX1__`);
  if (!response.ok) throw new Error("Error al cargar las opciones");
  const datos = await response.json();
  return datos.__AUX1__; // ← si responde sin nombre adentro: borrá el punto y la palabra
}

export async function getOpciones2() {
  const response = await fetch(`${API_BASE}/__AUX2__`);
  if (!response.ok) throw new Error("Error al cargar las opciones");
  const datos = await response.json();
  return datos.__AUX2__; // ← si responde sin nombre adentro: borrá el punto y la palabra
}
```

#### H14. `react/src/hooks/use__LISTA_CAP__.js`  ·  CON FILTROS

```js
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)  ·  versión CON FILTROS
// Si hay un solo select: borrá las líneas "← SELECT 2". Si no hay buscador: borrá las líneas "← BUSCADOR"
// y en la línea "← SIN BUSCADOR" sacale las dos barras // del principio.
import { useState, useEffect } from "react";
import { get__LISTA_CAP__ } from "../services/api";
import { useDebounce } from "./useDebounce"; // ← BUSCADOR

export function use__LISTA_CAP__(filtros = {}) {
  const [lista, setLista] = useState([]);
  const [cargando, setCargando] = useState(true);
  const [error, setError] = useState(null);

  const textoConEspera = useDebounce(filtros.__Q3__, 500); // ← BUSCADOR
  // const textoConEspera = ""; // ← SIN BUSCADOR

  useEffect(() => {
    async function cargar() {
      try {
        setCargando(true);
        setError(null);
        const datos = await get__LISTA_CAP__({
          __Q1__: filtros.__Q1__,
          __Q2__: filtros.__Q2__, // ← SELECT 2
          __Q3__: textoConEspera,
        });
        setLista(datos);
      } catch (e) {
        setError("No pudimos cargar los datos");
      } finally {
        setCargando(false);
      }
    }
    cargar();
  }, [filtros.__Q1__, filtros.__Q2__, textoConEspera]);

  return { lista, cargando, error };
}
```

#### H15. `react/src/hooks/useDebounce.js`  ·  CON FILTROS

```js
// PASO 1 · COPIAR TAL CUAL (solo si hay buscador de texto)
import { useState, useEffect } from "react";

export function useDebounce(valor, espera = 500) {
  const [valorConRetraso, setValorConRetraso] = useState(valor);

  useEffect(() => {
    const temporizador = setTimeout(() => setValorConRetraso(valor), espera);
    return () => clearTimeout(temporizador);
  }, [valor, espera]);

  return valorConRetraso;
}
```

#### H16. `react/src/components/Filtros.jsx`  ·  CON FILTROS

```jsx
// PASO 2 · REEMPLAZAR (Ctrl+H con la ficha)  ·  versión CON FILTROS
// Si hay un solo select: borrá desde "SELECT 2: desde acá" hasta "SELECT 2: hasta acá" y las líneas "← SELECT 2".
// Si no hay buscador: borrá desde "BUSCADOR: desde acá" hasta "BUSCADOR: hasta acá".
import { useState, useEffect } from "react";
import { getOpciones1, getOpciones2 } from "../services/api";

// (opcional, 1 minuto) entre las comillas: index.html → Ctrl+F <select → el texto de la primera <option value="">
// de cada select, y el placeholder="…" del buscador. Si lo dejás así también anda.
const TEXTO_SELECT1 = "Todos";
const TEXTO_SELECT2 = "Todos";
const TEXTO_BUSCADOR = "Buscar...";

function Filtros({ onFilterChange }) {
  const [opciones1, setOpciones1] = useState([]);
  const [opciones2, setOpciones2] = useState([]);
  const [filtros, setFiltros] = useState({ __Q1__: "", __Q2__: "", __Q3__: "" });

  useEffect(() => {
    getOpciones1().then(setOpciones1).catch(() => setOpciones1([]));
    getOpciones2().then(setOpciones2).catch(() => setOpciones2([])); // ← SELECT 2
  }, []);

  const cambiar = (campo, valor) => {
    const nuevos = { ...filtros, [campo]: valor };
    setFiltros(nuevos);
    onFilterChange(nuevos);
  };

  // Las clases (filters, filter-select, search-input): si en el index.html son otras, cambialas acá abajo
  return (
    <div className="filters">
      <select
        className="filter-select"
        value={filtros.__Q1__}
        onChange={(e) => cambiar("__Q1__", e.target.value)}
      >
        <option value="">{TEXTO_SELECT1}</option>
        {opciones1.map((opcion) => (
          <option key={opcion} value={opcion}>
            {opcion}
          </option>
        ))}
      </select>

      {/* SELECT 2: desde acá */}
      <select
        className="filter-select"
        value={filtros.__Q2__}
        onChange={(e) => cambiar("__Q2__", e.target.value)}
      >
        <option value="">{TEXTO_SELECT2}</option>
        {opciones2.map((opcion) => (
          <option key={opcion} value={opcion}>
            {opcion}
          </option>
        ))}
      </select>
      {/* SELECT 2: hasta acá */}

      {/* BUSCADOR: desde acá */}
      <input
        type="text"
        className="search-input"
        placeholder={TEXTO_BUSCADOR}
        value={filtros.__Q3__}
        onChange={(e) => cambiar("__Q3__", e.target.value)}
      />
      {/* BUSCADOR: hasta acá */}
    </div>
  );
}

export default Filtros;
```

#### H17. `react/src/components/__ITEM_CAP__Card.jsx`  ·  CON FILTROS

```jsx
// PASO 2 · REEMPLAZAR (ya anda con lo provisorio)  ·  PASO 4 · PEGAR HTML (la tarjeta)
import { Link } from "react-router-dom";

function __ITEM_CAP__Card({ __ITEM__ }) {
  /* ═══ PEGAR ACÁ (si hay): LO DE ARRIBA DEL HTML ═══
     SALE DE: el mismo JS de donde sacás la tarjeta → la función que la arma
              → desde la línea siguiente a su { de apertura hasta la línea anterior al return
              (líneas como const nombre = algo.nombre  o  const { a, b } = algo)
     Si "algo" no se llama __ITEM__, cambiá esa palabra por __ITEM__.
     Si el HTML usa una función que no copiaste (la consola dice "... is not defined"):
     buscala en el mismo JS y copiala entera acá también.
     Si no hay nada, borrá este comentario */

  return (
    <>
      {/* ═══ PEGAR ACÁ: LA TARJETA ═══
          SALE DE: el JS que pide la lista (el que tiene fetch a /api/__URL__) → Ctrl+F card
                   → la función o el .map que devuelve el HTML de UNA tarjeta
          DESDE: lo que sigue al ` de apertura   HASTA: lo anterior al ` de cierre
          AL TRADUCIR: el <div> de afuera que tiene onclick="…" pasa a ser el <Link> (con su mismo className):
                       <Link to={`/__RUTA__/${__ITEM__.__ID_CAMPO__}`} className="…">  …  </Link>
                       (si en vez de onclick hay un <a href="…?id=…">, ese <a> es el que pasa a <Link>)
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <Link
        to={`/__RUTA__/${__ITEM__.__ID_CAMPO__}`}
        style={{ display: "block", background: "#fff", color: "#222", padding: "8px", margin: "8px 0" }}
      >
        {__ITEM__.__NOMBRE__}
      </Link>
      {/* ═══ fin provisorio ═══ */}
    </>
  );
}

export default __ITEM_CAP__Card;
```

#### H18. `react/src/pages/Home.jsx`  ·  CON FILTROS

```jsx
// PASO 2 · REEMPLAZAR  ·  versión CON FILTROS (selects, buscador y tarjetas)
import { useState } from "react";
import Filtros from "../components/Filtros";
import __ITEM_CAP__Card from "../components/__ITEM_CAP__Card";
import Loading from "../components/Loading";
import ErrorMessage from "../components/ErrorMessage";
import { use__LISTA_CAP__ } from "../hooks/use__LISTA_CAP__";

function Home() {
  const [filtros, setFiltros] = useState({ __Q1__: "", __Q2__: "", __Q3__: "" });
  const { lista, cargando, error } = use__LISTA_CAP__(filtros);

  return (
    <div className="container">{/* ← si en index.html la pantalla de inicio está dentro de un div con otro class, cambialo */}
      <Filtros onFilterChange={setFiltros} />

      {cargando && <Loading />}
      {error && <ErrorMessage message={error} />}

      {!cargando && !error && lista.length === 0 && (
        <p className="empty-message">
          No se encontraron resultados.{/* ← (opcional) el texto de sin resultados del JS viejo: Ctrl+F empty-message */}
        </p>
      )}

      <div className="">{/* ← entre las comillas: el class del div donde el JS metía las tarjetas (index.html, Ctrl+F grid) */}
        {lista.map((x) => (
          <__ITEM_CAP__Card key={x.__ID_CAMPO__} __ITEM__={x} />
        ))}
      </div>
    </div>
  );
}

export default Home;
```

#### H19. `react/src/pages/Recientes.jsx`  ·  RECIENTES · LISTA

```jsx
// PASO 2 · REEMPLAZAR  ·  PASO 4 · PEGAR HTML (la pantalla de recientes)
// Versión LISTA: muestra lo guardado, sin volver a pedir nada al servidor.
// (Si la rúbrica dice "cruzar con la API" o "grilla de tarjetas", usá la otra versión de Recientes.)
import { Link } from "react-router-dom";
import { use__LISTA_CAP__Recientes } from "../hooks/use__LISTA_CAP__Recientes";

function Recientes() {
  const { recientes, limpiarRecientes } = use__LISTA_CAP__Recientes();

  const itemsRecientes = recientes.map((r) => (
    <li key={r.id}>
      <Link to={`/__RUTA__/${r.id}`}>
        {r.nombre} - {r.fecha}
      </Link>
    </li>
  ));

  return (
    <>
      {/* ═══ PEGAR ACÁ: LA PANTALLA DE RECIENTES ═══
          SALE DE: index.html (o la pantalla vieja que muestra el historial) → Ctrl+F historial
                   → desde el título del historial hasta el último botón del historial
                   (si hay una <section> de recientes: lo de ADENTRO, la etiqueta <section> no va)
          AL TRADUCIR: el <ul> vacío → <ul>{itemsRecientes}</ul>
                       el botón de limpiar → onClick={limpiarRecientes}
          Al pegar, borrá desde esta marca hasta "fin provisorio" */}
      <div className="container">
        <h2>Recientes</h2>
        <ul>{itemsRecientes}</ul>
        {recientes.length > 0 && <button onClick={limpiarRecientes}>Limpiar historial</button>}
      </div>
      {/* ═══ fin provisorio ═══ */}
    </>
  );
}

export default Recientes;
```

#### H20. `react/src/pages/Recientes.jsx`  ·  RECIENTES · CRUZAR CON LA API

```jsx
// PASO 2 · REEMPLAZAR  ·  versión CRUZAR CON LA API: vuelve a pedir cada guardado al servidor y muestra tarjetas.
// Usala si la rúbrica dice "cruzar con la API" o "grilla de tarjetas". Necesita la tarjeta (__ITEM_CAP__Card.jsx).
import { useState, useEffect } from "react";
import { get__ITEM_CAP__ } from "../services/api";
import { use__LISTA_CAP__Recientes } from "../hooks/use__LISTA_CAP__Recientes";
import __ITEM_CAP__Card from "../components/__ITEM_CAP__Card";
import Loading from "../components/Loading";

function Recientes() {
  const { recientes, limpiarRecientes } = use__LISTA_CAP__Recientes();
  const [lista, setLista] = useState([]);
  const [cargando, setCargando] = useState(true);

  useEffect(() => {
    async function cargar() {
      setCargando(true);
      const resultados = await Promise.all(
        recientes.map((r) => get__ITEM_CAP__(r.id).catch(() => null))
      );
      setLista(resultados.filter((uno) => uno !== null));
      setCargando(false);
    }
    cargar();
  }, [recientes]);

  return (
    <div className="container">{/* ← si en index.html la pantalla de recientes está dentro de un div con otro class, cambialo */}
      <h2 className="page-title">
        Recientes{/* ← (opcional) el texto del título de la pantalla de recientes del index.html */}
      </h2>

      {recientes.length > 0 && <button onClick={limpiarRecientes}>Limpiar historial</button>}

      {cargando && <Loading />}

      {!cargando && lista.length === 0 && (
        <p className="empty-message">
          Todavía no viste ninguno.{/* ← (opcional) el texto de "vacío" de la pantalla de recientes (Ctrl+F empty-message) */}
        </p>
      )}

      <div className="">{/* ← entre las comillas: el class del div donde iban las tarjetas de recientes (el mismo de la grilla de inicio, casi siempre) */}
        {lista.map((x) => (
          <__ITEM_CAP__Card key={x.__ID_CAMPO__} __ITEM__={x} />
        ))}
      </div>
    </div>
  );
}

export default Recientes;
```


---

## 9. OPCIONAL: componente extra que pide la rúbrica

#### `react/src/components/__EXTRA__.jsx`

```jsx
// OPCIONAL · solo si la rúbrica pide separar un pedazo en su propio componente (ej. Navbar, Banner, Section)
// y sobra tiempo. __EXTRA__ = el nombre que dice la rúbrica (con mayúscula). El archivo se llama igual.
// En LOGIN cambiá "export default function" por "export function" y quitá "export default" de abajo.
import { Link, NavLink } from "react-router-dom";

export default function __EXTRA__({ children }) {
  return (
    <>
      {/* ═══ PEGAR ACÁ: EL PEDAZO QUE PIDE LA RÚBRICA ═══
          SALE DE: el archivo donde ya lo tenés pegado (Layout, Header, la Home…): cortalo de ahí y pegalo acá.
          En el archivo de donde lo cortaste escribí <__EXTRA__ /> en su lugar, y arriba de todo:
          import __EXTRA__ from "./__EXTRA__";   (o "../components/__EXTRA__" si estás en pages)
          Si el pedazo usaba algo de ese archivo (por ejemplo {areaLogin}), pasalo así: <__EXTRA__>{areaLogin}</__EXTRA__>
          y acá escribí {children} donde iba */}
    </>
  );
}
```


---

## Anexo A. Reglas HTML → JSX

| HTML viejo | JSX |
|---|---|
| `class="x"` | `className="x"` |
| `${x}` | `{x}` — **sin comillas**: `src={x}`, nunca `src="{x}"` |
| `<img ...>`, `<input ...>`, `<br>` | `<img ... />`, `<input ... />`, `<br />` |
| `onerror="..."`, `onclick="..."` | se borran |
| `<a href="algo.html?id=${id}">` | `<Link to={`/__RUTA__/${id}`}>` |
| `${cond ? \`...\` : ""}` | `{cond && (...)}` |
| `${lista.map(x => \`<li>${x}</li>\`).join("")}` | `{lista.map((x, i) => <li key={i}>{x}</li>)}` |
| texto con variable dentro de un atributo: `title="Hola ${x}"` | `title={\`Hola ${x}\`}` |
| `$${precio}` (signo pesos delante) | `${precio}` (el primer `$` es texto) |
| `frameborder`, `allowfullscreen` | `frameBorder`, `allowFullScreen` |
| `style="color: red; margin-top: 2rem"` | `style={{ color: "red", marginTop: "2rem" }}` |
| `for="x"` (en `<label>`) | `htmlFor="x"` |
| `<!-- comentario -->` | `{/* comentario */}` o borrarlo |
| `<tr>` suelto adentro de `<table>` (sin `<thead>`/`<tbody>`) | envolver las filas en `<tbody> ... </tbody>` (React avisa en consola si falta) |
| Un campo que es un **objeto** (`{ a: "x", b: "y" }`) | no se puede escribir `{objeto}`; escribir el campo de adentro: `{objeto.a}` |
| Dos o más elementos hermanos sin un padre | envolverlos en `<>` … `</>` |

**El `id` que viene de la dirección (`useParams()`) siempre es texto**, aunque en los datos sea un número. Si hay que compararlo con un número: `Number(id)` o comparar como texto `String(x.id) === id`.

**`NavLink`** agrega solo la clase `active` al link de la página actual. Si el CSS viejo usa otra clase para "página activa", se escribe en el className del NavLink.

**En criollo:** `class` pasa a `className`, `${}` pasa a `{}` sin comillas, las etiquetas sueltas se cierran con `/>` y lo que toca la pantalla a mano se borra.

---

## Anexo B. Situaciones que pueden aparecer

- **El esqueleto de React trae archivos que no son de este parcial** (nombres de otra cosa, CSS con otros colores) → borrar lo que sobra y reemplazar el CSS por el del modelo viejo (pasos previos).
- **`npm install` falla en `server/`** → abrir `server/package.json`: si tiene dos bloques `{ ... }` pegados, borrar el segundo.
- **El servidor arranca en otro puerto** → mirar la línea `PORT` y lo que imprime la terminal; ese número va en `__PUERTO__`.
- **Las imágenes no cargan y su ruta empieza con `./` o `/`** (no con `http`) → las sirve el servidor: anteponer `` `http://localhost:__PUERTO__/` `` (poner el número ya reemplazado).
- **El JS viejo lee un archivo `data/*.json` directo** → en React se usa la ruta del servidor (`/api/...`) que devuelve lo mismo.
- **Hay elementos con el id repetido** → React se queja de "keys" repetidas; usar `key={`${x.id}-${i}`}`.
- **Un dato que el detalle muestra no viene en `/api/algo/:id`** → ver cómo lo consigue el JS viejo (suele pedir también la lista) y en LOGIN la lista ya está en `lista` adentro del detalle (la plantilla la trae siempre); en HISTORIAL preguntá.
- **El README pide algo que el servidor no tiene** (una búsqueda, un orden) → avisar y decidir; no inventar rutas.
- **La ruta de detalle es siempre `/:ruta/:id`**, y en el componente `useParams()` devuelve `{ id }`. Aunque el servidor use otro nombre para el id, en la dirección del navegador se escribe `:id`.
- **Las tarjetas llevan `<Link>`**, no `useNavigate`. `useNavigate` queda solo para botones como "Volver".
- **El profe pidió armar `App.jsx` temprano** con páginas provisorias (un `<h1>` por página) para probar las rutas antes de las pantallas reales.
- **Recientes / historial:** se guardan `{ id, nombre, fecha }`. Si la rúbrica dice "cruzar con la API", se usa la versión "cruzar con la API" de `Recientes.jsx` (vuelve a pedir cada id al servidor).

**Mis errores frecuentes:**
1. Confundir la ruta del servidor (`/api/algo`) con la del navegador (`/algo/:id`).
2. Al reemplazar un token, borrar el texto pegado al lado (`__LISTA_CAP__RecientesContext`).
3. Inventar textos en vez de copiarlos del `index.html` o del JS.
4. Confundir la lista (plural) con el ítem (singular).
5. Mayúsculas en los nombres de campos.
6. Comillas alrededor de llaves (`src="{x}"`) y dejar `onerror`.
7. Copiar el `div` de afuera de la tarjeta (con `onclick`) adentro del `<Link>`.
8. Crear archivos escribiendo la ruta completa como nombre.
9. Olvidar `npm install` en alguna de las dos carpetas.

---

## Anexo C. Errores comunes de consola

**Cómo leerla:** F12 → pestaña **Consola** (y **Red** si hay un número 404/500). Buscá el mensaje en la columna "Qué dice", mirá "Qué significa" y hacé lo de "Qué hago".
Todos los mensajes de esta tabla **se reprodujeron a propósito** en un proyecto armado con las plantillas (Chrome + Vite). Los textos pueden variar un poco en la versión de tu máquina.

### A. Pantalla en blanco (la consola muestra un error rojo)

| Qué dice | Qué significa | Qué hago |
|---|---|---|
| `X is not defined` (ej. `formatAlgo is not defined`) | Usé algo que no copié: una función o una variable del JS viejo | Buscar `X` en el JS viejo; si es `function X(...)` o `const X = ...`, copiarla en la marca **LO DE ARRIBA DEL HTML** de ese archivo (arriba del `return`) |
| `Cannot read properties of undefined (reading 'length')` y la consola dice `The above error occurred in the <Home> component` | El dato todavía no llegó o llegó con otra forma: casi siempre el nombre de `__WRAP_LISTA__` / `__WRAP__` está mal | Comparar con el `res.json({ ... })` del servidor; corregir el nombre en `services/api.js` |
| `Cannot read properties of undefined (reading 'algo')` | Estoy leyendo un campo de algo que no existe (nombre mal escrito, o falta un `?.`) | Mirar la línea y el archivo que marca la consola; revisar el nombre del campo contra el dato real |
| `Objects are not valid as a React child (found: object with keys {...})` | Escribí `{algo}` pero `algo` es un objeto, no un texto | Escribir el campo de adentro (`{algo.campo}`); mirar las claves que lista el error |
| `usarAlgo debe usarse dentro de AlgoProvider` (el texto exacto es el del hook de la plantilla) | Falta envolver con el Provider en `App.jsx`, o lo envolví mal | Revisar que `App.jsx` tenga `<Provider>` rodeando a `<BrowserRouter>` y a todas las rutas; revisar la ruta del import |

### B. Pantalla en blanco o cartel rojo de Vite (no abre ni la página)

| Qué dice | Qué significa | Qué hago |
|---|---|---|
| `Failed to resolve import "../components/X" from "src/pages/Y.jsx". Does the file exist?` | El nombre o la carpeta del import no coincide con el archivo | Comparar letra por letra con el nombre del archivo en el explorador (mayúsculas incluidas) y con el token reemplazado |
| `[plugin:vite:react-babel] ... Unterminated JSX contents. (línea:col)` | Falta cerrar una etiqueta (muy común `<img ...>` sin `/>`) | Ir a la línea que marca; cerrar con `/>` o agregar el `</etiqueta>` que falta |
| Otros `[plugin:vite:react-babel] ...` | Error de sintaxis en JSX: llave, paréntesis o etiqueta sin cerrar | Ir a la línea y columna que marca; revisar lo último que pegaste |

### C. La pantalla se ve pero algo anda mal (avisos en la consola)

| Qué dice | Qué significa | Qué hago |
|---|---|---|
| `Warning: Invalid DOM property class. Did you mean className?` | Quedó un `class=` del HTML viejo | Cambiar a `className=` |
| `Warning: Encountered two children with the same key` | Hay elementos con el mismo `id` usados como `key` | Usar `key={`${x.id}-${i}`}` (Anexo B) |
| `Warning: validateDOMNesting(...): <tr> cannot appear as a child of <table>. Add a <tbody>...` | Filas `<tr>` sin `<tbody>` | Envolver las filas en `<tbody>` |
| Aviso amarillo `React Router Future Flag Warning ...` | Aviso de versión, **no es un error** | Ignorarlo |
| Las imágenes salen rotas y no hay mensaje | Escribí `src="{x}"` (con comillas) o la ruta de la imagen es del servidor y falta anteponer `http://localhost:PUERTO/` | `src={x}` sin comillas; ver regla de imágenes (Anexo B) |

### D. Problemas con el servidor / los datos

| Qué dice | Qué significa | Qué hago |
|---|---|---|
| `Failed to fetch` / `net::ERR_CONNECTION_REFUSED` | El servidor **no está corriendo** o `__PUERTO__` está mal | Mirar la terminal 1: ¿dice que escucha en el puerto? Comparar con la línea `PORT` y con `services/api.js` o `api/client.js` |
| `Failed to load resource: ... 404 (Not Found)` y en Red se ve `/api/algo` | La ruta que pido (`__URL__`) no existe en el servidor | Comparar con el `app.get('/api/...')` del servidor |
| 404 en Red con `/api/algo/undefined` | El `id` llegó vacío: `__ID_CAMPO__` mal en el `Link` de la tarjeta, o la ruta del navegador no usa `:id` | Revisar `to={`/__RUTA__/${item.__ID_CAMPO__}`}` en la tarjeta y `path="/__RUTA__/:id"` en `App.jsx` |
| No hay ningún error claro, pero la pantalla dice "No hay datos" / queda vacía | Suele ser que la dirección base del servidor está mal escrita (por ejemplo `/api` sin `http://localhost:PUERTO`): lo que vuelve no son los datos | F12 → Red → clic en la petición `/api/...` → pestaña Respuesta: si no es el JSON esperado, corregir la dirección base (`api/client.js` o `services/api.js`) para que empiece con `http://localhost:__PUERTO__/api` |
| La página de detalle dice "No encontrado" | El id no llegó (ver 404 con `undefined`) o el id no existe en el servidor | Misma revisión que arriba; probar la dirección `/api/algo/ID` a mano en el navegador |

**Orden para investigar:** 1) ¿el servidor está corriendo? 2) F12 → Consola, leer **el primer** error rojo (los de abajo suelen ser consecuencia). 3) Si dice un archivo y una línea, ir ahí. 4) Si es un 404, F12 → Red → mirar la dirección exacta que se pidió.

**En criollo:** el primer error rojo de la consola dice casi siempre en qué archivo y qué falta; el 404 dice qué dirección se pidió mal.

---



---

## Qué se probó y qué no (plantillas v2)

### Probado

Con estas plantillas se armaron los 7 modelos de práctica **dos veces**, haciendo los mismos pasos de la sección 1:

- **Completo:** pasos 0 a 4, con el HTML viejo pegado y traducido en cada marca.
- **Solo lo mecánico ("piso"):** pasos 0 a 3, sin pegar nada de HTML (quedan todos los provisorios).

| Modelo | Familia y versiones | Completo | Solo lo mecánico |
|---|---|---|---|
| Modelo 1 | LOGIN, OPCIÓN B | 19 de 19 | 19 de 19 |
| Modelo 2 | LOGIN, OPCIÓN C + footer | 18 de 18 | 18 de 18 |
| Modelo 3 | LOGIN, OPCIÓN A + footer + dato que sale de la lista | 19 de 19 | 19 de 19 |
| Modelo 4 | LOGIN, OPCIÓN B + footer | 19 de 19 | 19 de 19 |
| Modelo 5 | HISTORIAL sin filtros, recientes LISTA, detalle suelto | 17 de 17 | 17 de 17 |
| Modelo 6 | HISTORIAL con filtros, recientes CRUZAR + footer | 26 de 26 | 26 de 26 |
| Modelo 7 | HISTORIAL con filtros, recientes CRUZAR + footer | 26 de 26 | 26 de 26 |
| Variante de prueba | HISTORIAL sin filtros + recientes CRUZAR (con la tarjeta de con filtros), lista **suelta** | 19 de 19 | 19 de 19 |

**En todos:**
- `npm install` y `vite build` sin errores.
- Ctrl+F `__`, las marcas `═══` y `←` dan 0 en `react/src`.
- Las pruebas se hicieron con servidor y Vite reales y un navegador automático.

**Qué revisan las pruebas:**
- **LOGIN:**
  - Cantidad de tarjetas.
  - Tarjeta → `/ruta/id` correcto, sin recargar.
  - El detalle muestra el nombre, abre con F5 y tiene Volver.
  - Id inexistente y 404.
  - Login mal (error) y bien (Bienvenido).
  - Sesión guardada en `localStorage` con `__CLAVE__`, que sigue al recargar.
  - Cerrar sesión.
- **HISTORIAL:**
  - Select y botón, o tarjetas.
  - Cada filtro y el buscador piden lo mismo que la API, y el buscador espera.
  - Mensaje sin resultados.
  - Recientes guarda `{ id, nombre, fecha }` sin repetir, el último primero, tope 15, y sigue al recargar.
  - `/recientes` muestra lo visitado; "Limpiar historial" lo vacía.
  - Id inexistente, 404, y el link del header a Recientes.
- **Las dos familias:** 0 errores de JavaScript en la consola.

### NO probado

1. **Imágenes, iconos y CSS externos:** sin internet en el entorno de prueba, no los vi cargados.
2. **Tu trabajo a mano en VS Code:** los archivos los escribió un programa siguiendo los pasos. Copiar, pegar y Ctrl+H a mano no se probó.
3. **Los casos "un solo select" y "sin buscador"** (las líneas `← SELECT 2` / `← BUSCADOR`): están marcados pero ningún modelo los tiene, así que no se probaron.
4. **El componente extra opcional** (`__EXTRA__.jsx`) no se probó.
5. **Lo provisorio se ve feo a propósito:** cajas blancas con los datos crudos. Anda, pero no se parece al viejo. El parecido se logra solo pegando el HTML.
6. **Un caso que no es copiar y pegar:** en un modelo de práctica, el detalle muestra un dato que el JS viejo saca **buscando en la lista**. La plantilla ya trae la lista (`lista`), pero adaptar esa búsqueda no es mecánico. Si te pasa, preguntá.
7. **Nombres que no encajan en el molde** de la rúbrica (`CardClase`, `useLogin`, `useHistorialConsultas`): la plantilla usa `XxxCard` / `useAuth` / `useXxxRecientes`. Renombrar no da puntos solo; dejalo para el final si sobra tiempo.
8. **Parciales con algo que ningún modelo trae** (otra forma de respuesta, otra pantalla): las reglas cubren lo que aparece en los 7 modelos. Para lo nuevo, preguntá con el archivo real abierto.
9. **La duración del parcial** sigue sin confirmar.
