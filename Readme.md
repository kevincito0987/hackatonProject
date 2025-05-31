# 🌱 EcoMarket — Comercio con propósito, tecnología con impacto 🌱

**Frase estelar:**
 **“Tecnología que transforma residuos en oportunidades. Hecho con innovación, conciencia y amor por el planeta.”** 🌎💚⚡

------

## 🧠 ¿Qué es EcoMarket?

**EcoMarket** es una plataforma de comercio electrónico pensada para la economía circular.
 Permite a los usuarios:

- Reciclar sus dispositivos electrónicos usados mediante **IA de visión computacional**.
- Recibir crédito económico por su valor estimado.
- Comprar productos reacondicionados o ecológicos dentro del mismo marketplace.
- Visualizar su impacto ambiental de forma clara y motivadora.

------

## 🧩 Proyecto original y evolución

Este proyecto fusiona 2 ideas base de la hackathon:

1. "Más ecológico" – Sistema de reciclaje electrónico con cotización, recolección y trazabilidad.
2. "No hay comercio como el comercio electrónico" – Framework para que usuarios puedan comprar/vender sin fricción.

**EcoMarket** expande estas ideas con inteligencia artificial, trazabilidad, internacionalización, y monetización responsable.

------

## 🛠️ Tecnologías utilizadas

- **Frontend:** React.js + TailwindCSS + Vite
- **Backend:** FastAPI (Python) + Uvicorn
- **Visión por Computadora:** YOLOv8 (con entrenamiento desde Roboflow)
- **Base de datos:** PostgreSQL + Redis
- **Hosting:** Netlify (frontend), Render (backend)
- **Monetización:** RevenueCat
- **Internacionalización:** Lingo
- **Blockchain trazabilidad:** Algorand / IPFS
- **Monitoreo:** Sentry
- **Generación UI:** 21st.dev
- **Voz personalizada:** ElevenLabs
- **Gestión del proyecto:** Git + GitHub + GitHub Projects

------

## 📐 Arquitectura de software

Sistema modular por capas que separa claramente:

1. **Frontend React (SPA):** modular, basado en componentes, con hooks personalizados.
2. **Backend FastAPI (Python):**
   - API Layer (endpoints)
   - Service Layer (lógica de negocio)
   - Repository Layer (acceso a DB)
   - AI Layer (detección de dispositivos con YOLOv8)
   - Integration Layer (pagos, autenticación, etc.)
3. **Microservicio IA (YOLOv8):** recibe imagen, responde cotización estimada.
4. **Integraciones externas:** Stripe, Algorand, IPFS, Firebase Auth, Lingo, ElevenLabs, etc.

------

## 📦 Estructura del proyecto

ecomarket/
│
├── frontend/
│   ├── src/
│   │   ├── components/           # Atomic components (atoms/molecules/etc.)
│   │   ├── hooks/                # Custom React hooks
│   │   ├── pages/                # Page-level components
│   │   ├── services/             # API requests
│   │   ├── context/              # Estado global
│   │   └── utils/                # Funciones auxiliares
│   └── public/
│
├── backend/
│   ├── app/
│   │   ├── api/                  # Rutas FastAPI
│   │   ├── services/             # Lógica de negocio
│   │   ├── models/               # Pydantic schemas
│   │   ├── db/                   # Repositorios y conexión a DB
│   │   ├── integrations/         # Stripe, Firebase, etc.
│   │   └── ai/                   # Modelo YOLOv8 y predicciones
│   └── main.py
│
├── docker/
│   └── docker-compose.yml
└── README.txt (este archivo)

------



## 📦 Estructura del Proyecto — Implementación + Patrones de Diseño

### `ecomarket/`

------

### 🔹 `frontend/src/components/`

**Rol:** Componentes visuales reutilizables
 **Patrón aplicado:** Atomic Design

- **Atoms:** `Button`, `Input`, `Icon`
- **Molecules:** `ProductCard`, `UploadBox`
- **Organisms:** `MarketplaceGrid`, `UserPanel`, `Header`

**Ejemplo:** `ProductCard.tsx` muestra un producto reacondicionado y es reutilizado en todo el marketplace.

------

### 🔹 `frontend/src/hooks/`

**Rol:** Lógica personalizada reutilizable
 **Patrón aplicado:** Custom Hooks Pattern
 **Ejemplos:**

- `useRecycleEstimate()` → Llama a la API para obtener cotización por imagen.
- `useUserCredits()` → Recupera créditos disponibles del usuario.

------

### 🔹 `frontend/src/pages/`

**Rol:** Composición de páginas
 **Patrón aplicado:** Container–Presenter Pattern
 **Ejemplo:**
 `RecyclePage.tsx` gestiona datos y lógica → usa `RecycleForm.tsx` (presenta UI).

------

### 🔹 `frontend/src/services/`

**Rol:** Abstracción de llamadas API
 **Patrón aplicado:** Service Layer
 **Ejemplo:**

```
tsCopiarEditarexport async function getEstimate(file) {
  const formData = new FormData();
  formData.append("image", file);
  const res = await fetch("/api/estimate", { method: "POST", body: formData });
  return res.json();
}
```

------

### 🔹 `frontend/src/context/`

**Rol:** Manejo de estado global
 **Patrón aplicado:** Context Provider
 **Ejemplo:** `UserProvider.tsx` mantiene el estado del usuario logueado y sus créditos.

------

### 🔹 `frontend/src/utils/`

**Rol:** Funciones auxiliares comunes
 **Ejemplo:** `formatCredits(150)` → `$150 EcoCredits`

------

### 🔹 `backend/app/api/`

**Rol:** Rutas y controladores FastAPI
 **Patrón aplicado:** Modular Routing
 **Ejemplo:**

```
pythonCopiarEditar@router.post("/estimate")
async def estimate(file: UploadFile):
    result = ai.predict(file)
    return {"value": result.price}
```

------

### 🔹 `backend/app/services/`

**Rol:** Lógica de negocio separada de la API
 **Patrón aplicado:** Service Layer Pattern
 **Ejemplo:**
 `recycle_service.py` procesa la imagen, llama a IA y devuelve cotización.

------

### 🔹 `backend/app/models/`

**Rol:** Validación de datos con Pydantic
 **Patrón aplicado:** DTO/Schema Pattern
 **Ejemplo:**

```
pythonCopiarEditarclass EstimateRequest(BaseModel):
    image: str
```

------

### 🔹 `backend/app/db/`

**Rol:** Acceso y operaciones a la base de datos
 **Patrón aplicado:** Repository Pattern
 **Ejemplo:**
 `DeviceRepository.py` contiene funciones como `save_estimate()`, `get_history()`.

------

### 🔹 `backend/app/ai/`

**Rol:** Integración con YOLOv8 u otro modelo
 **Patrón aplicado:** Adapter Pattern
 **Ejemplo:**
 `yolo_adapter.py` contiene la función `predict(image)` que convierte imagen en predicción de clase + valor.

------

### 🔹 `backend/app/integrations/`

**Rol:** Encapsula servicios externos
 **Patrón aplicado:** Adapter + Facade Pattern
 **Ejemplos:**

- `stripe_adapter.py` para cobros y pagos.
- `lingo_adapter.py` para traducción automática.

------

### 🔹 `docker/`

Contiene `docker-compose.yml` para levantar servicios en local.

------

### 🔹 `docs/assets/`

Material visual, diagramas, pitch, mockups, etc.

------

### 🔹 `README.txt`

Documentación base, cronograma, instrucciones, estructura y arquitectura.

------

## ✅ Resumen de Patrones Aplicados

| Carpeta             | Patrón                | Propósito                             |
| ------------------- | --------------------- | ------------------------------------- |
| `components/`       | Atomic Design         | Modulariza y escala UI                |
| `hooks/`            | Custom Hooks          | Reutiliza lógica en frontend          |
| `pages/`            | Container–Presenter   | Separa lógica y presentación          |
| `services/ (front)` | Service Layer         | Limpia llamadas a backend             |
| `context/`          | Context Provider      | Maneja estado global                  |
| `api/`              | Modular Routing       | Organiza endpoints                    |
| `services/ (back)`  | Service Layer         | Lógica desacoplada                    |
| `models/`           | DTO/Schema (Pydantic) | Validación estructurada               |
| `db/`               | Repository Pattern    | Acceso limpio a base de datos         |
| `ai/`               | Adapter Pattern       | Conecta IA sin acoplar lógica         |
| `integrations/`     | Adapter + Facade      | Control centralizado de APIs externas |

------

## 📆 Plan de desarrollo modular

**Duración:** del 2 al 30 de junio

- Módulo 1 (2–6 Jun) – Configuración de proyecto + estructura base
- Módulo 2 (7–12 Jun) – IA de cotización (YOLOv8) + backend FastAPI
- Módulo 3 (13–17 Jun) – E-commerce funcional (productos + créditos)
- Módulo 4 (18–23 Jun) – Internacionalización + trazabilidad blockchain
- Módulo 5 (24–30 Jun) – Integración total + monitoreo + pitch final

------

## ✅ Funcionalidades destacadas

- Subida de imagen del dispositivo a reciclar
- Estimación automática del valor con IA
- Recepción de crédito y carrito de compra ecológico
- Productos reacondicionados en catálogo
- Panel de impacto ambiental personalizado
- Trazabilidad de reciclaje en blockchain
- Voz personalizada y feedback dinámico

------

## 🔄 Control de versiones y gestión

- Repositorio: Git + GitHub (público)
- Flujo Git: ramas por módulo (`module/1-init`, `module/2-ai`, etc.)
- Issues: registrados en GitHub Issues
- Tareas y sprints: organizadas en GitHub Projects (tablero Kanban)
- Commits: estilo semántico (`feat:`, `fix:`, `chore:`)

------

## 👨‍💻 Desarrollo y créditos

Desarrollador principal:
 kevincito0987 – GitHub: https://github.com/kevincito0987

Agradecimientos a Bolt, Devpost y todos los sponsors por las herramientas, soporte y motivación.

------

## ✨ Frase estelar final

**“Tecnología que transforma residuos en oportunidades. Hecho con innovación, conciencia y amor por el planeta.”** 🌎💚⚡