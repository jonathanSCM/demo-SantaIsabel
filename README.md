# Santa Isabel — Taller

Prototipo de validación para un taller de confección de vestidos (quinceañeras,
bautizos, damas de honor, uniformes de gala, etc.). Une dos módulos en una sola
app: control de pedidos y producción (basado en el prototipo "Trama") y
cotizaciones con costeo detallado (tela, avíos, empaque, producción, curva de
tallas y variantes de color).

**No es el sistema final** — es un prototipo de un solo archivo, sin backend,
para validar el flujo con el cliente antes de definir el alcance del MVP.

## Cómo abrirlo

Es un solo archivo HTML sin dependencias ni backend. Podés:

- Abrir `index.html` directamente en el navegador, o
- Servirlo con GitHub Pages (Settings → Pages → Deploy from branch → `main` / `/root`), o
- Servirlo localmente:

```bash
python -m http.server 8080
```

Luego abrí <http://localhost:8080>.

### Despliegue con Docker / Coolify

El repo incluye un `Dockerfile` (nginx sirviendo `index.html` en el puerto 80).
En Coolify: crear una aplicación → tipo **Dockerfile** → apuntar a este repo y
branch `main` → deploy. No hace falta configurar variables de entorno ni build
command, es un solo archivo estático.

Para probarlo local:

```bash
docker build -t santa-isabel .
docker run -p 8080:80 santa-isabel
```

Luego abrí <http://localhost:8080>.

## Qué incluye

- **Tablero** — indicadores, alertas, cotizaciones pendientes, carga de los
  próximos 14 días y próximas entregas.
- **Esta semana** — Hoy · Próximos · Atrasados · Terminados.
- **Pedidos** — listado completo con filtros por estado, clienta y fecha.
- **Cotizaciones** — lista con estado (Borrador/Enviada/Aprobada/Rechazada),
  editor de costeo (tela, avíos, empaque, producción, curva de tallas,
  variantes de color, muestra y molde) y hoja de cotización exportable a PDF.
  Aprobar una cotización crea el pedido correspondiente automáticamente.
- **Calendario de entregas** — pedidos por fecha comprometida, con semáforo de
  carga.

Diseño **mobile-first**: navegación por pestañas inferiores y botón flotante en
pantallas chicas, barra lateral y tablas completas a partir de tablet/escritorio.

## Qué NO incluye

Inventario, kardex, facturación, compras, costos reales de insumos, CRM,
WhatsApp, IA ni persistencia de datos.

## Notas

- Los datos son **ficticios** y se generan relativos al día en que se abre, así
  que la demo nunca se ve desactualizada.
- No hay backend: al recargar, todo vuelve al estado inicial (salvo el
  borrador de una cotización en curso, que se guarda en el `localStorage` del
  navegador para poder exportarla a PDF).
