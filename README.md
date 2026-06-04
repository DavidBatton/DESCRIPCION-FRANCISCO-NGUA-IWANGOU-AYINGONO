# Tablero Kanban — TFG 📋

Aplicación web de gestión de tareas tipo Kanban desarrollada con **Angular 21** como herramienta de seguimiento del Trabajo de Fin de Grado: *Plataforma Musical de Guinea Ecuatorial*.

**Autor:** Francisco Ngua Iwangou AYINGONO — AAUCA 2026

---

## ¿Qué es?

Un tablero Kanban interactivo que visualiza el progreso de todas las tareas del TFG organizadas en 4 columnas y 5 fases de desarrollo. Incluye drag & drop, persistencia local y acordeones por fase.

---

## Tecnologías

| Componente       | Tecnología                          |
|------------------|-------------------------------------|
| Framework        | Angular 21.1.3                      |
| Drag & Drop      | Angular CDK — `@angular/cdk`        |
| Estilos          | CSS puro (sin framework)            |
| Iconos           | SVG inline (Lucide)                 |
| Persistencia     | `localStorage`                      |
| Fuente           | Inter (Google Fonts)                |
| Build            | Angular CLI 21.1.1                  |

---

## Estructura del tablero

### Columnas

| Columna       | Descripción                                    |
|---------------|------------------------------------------------|
| Backlog       | Tareas pendientes de iniciar                   |
| En progreso   | Tareas actualmente en desarrollo               |
| En revisión   | Tareas completadas pendientes de verificación  |
| Completado    | Tareas finalizadas (agrupadas por fase)        |

### Fases del TFG

| Fase | Nombre       | Tareas |
|------|--------------|--------|
| F1   | Análisis     | 6      |
| F2   | Diseño       | 7      |
| F3   | Backend      | 20     |
| F4   | Frontend     | 26     |
| F5   | Pruebas      | 10     |

---

## Funcionalidades

- **Drag & drop** entre columnas — arrastra desde el handle (⠿) que aparece al pasar el ratón sobre una tarjeta
- **Acordeones por fase** en la columna Completado — colapsa/expande grupos para reducir el scroll
- **Filtro por fase** — muestra solo las tareas de F1, F2, F3, F4 o F5
- **Barra de progreso** en tiempo real — muestra el porcentaje de tareas completadas
- **Nueva tarea** — botón en el header para añadir tareas personalizadas
- **Editar / Eliminar** tarjetas — botones visibles al hacer hover
- **Restaurar** — vuelve al estado inicial del TFG (con confirmación)
- **Persistencia** en `localStorage` — los cambios se guardan automáticamente entre sesiones

---

## Instalación y arranque

### Requisitos

- Node.js 18+
- npm 10+

### Pasos

```bash
# Entrar a la carpeta del proyecto
cd kanban-tfg

# Instalar dependencias (ya incluidas en node_modules)
npm install

# Arrancar el servidor de desarrollo
npm start
```

La aplicación queda disponible en `http://localhost:4200`.

---

## Comandos disponibles

```bash
npm start        # Servidor de desarrollo con hot reload
npm run build    # Compilar para producción (output en /dist)
npm test         # Ejecutar tests unitarios con Vitest
npm run watch    # Build en modo watch (desarrollo)
```

---

## Estructura del código

```
kanban-tfg/src/app/
├── app.ts                    # Componente raíz — lógica del tablero
├── app.html                  # Template — layout completo
├── app.css                   # Estilos — layout, columnas, tarjetas
├── models/
│   └── tarea.model.ts        # Interfaces: Tarea, Columna, FaseTarea
├── services/
│   └── kanban.service.ts     # Estado reactivo con signals + localStorage
└── data/
    └── tareas-iniciales.ts   # 69 tareas predefinidas del TFG
```

### Flujo de datos

```
tareas-iniciales.ts
       ↓
KanbanService (signal)  ←→  localStorage
       ↓
App component (computed)
       ↓
Template (columnas + tarjetas)
```

---

## Decisiones de diseño

**Scroll por columna, no por página** — cada columna tiene su propio scroll interno (`overflow-y: auto`). El tablero ocupa exactamente `100vh` usando una arquitectura `flex-column` en el componente raíz.

**`overflow-x: visible` en columnas** — permite que el `cdk-drag-preview` (que se adjunta al `<body>` durante el arrastre) sea visible sin quedar recortado por el contenedor.

**Acordeones en "Completado"** — la columna con más tareas (60+) se organiza en 5 grupos colapsables por fase para evitar scroll excesivo.

**Signals de Angular** — el estado del tablero usa `signal()` y `computed()` de Angular 17+ para reactividad sin NgRx.

---

## Licencia

Proyecto académico — TFG 2026. Uso interno.

---

## Contexto del TFG

Este tablero forma parte del Trabajo Fin de Grado **"Plataforma Musical de Guinea Ecuatorial"** de la Universidad Afro-Americana de África Central (AAUCA).

El proyecto principal incluye:
- **Backend** — 4 microservicios Spring Boot con integración MUNI Dinero
- **Frontend** — Aplicación Angular 21 con 3 roles (usuario, artista, admin)
- **Kanban** — Este tablero de seguimiento del desarrollo

**Autor:** Francisco Ngua Iwangou AYINGONO
- GitHub: [DavidBatton](https://github.com/DavidBatton)
- Email: davidngua.iwangou@gmail.com
