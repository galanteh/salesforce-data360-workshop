# Salesforce Data 360 Interactive Workshop

![Salesforce Data 360](https://img.shields.io/badge/Salesforce-Data%20360-00A1E0?style=flat-square&logo=salesforce&logoColor=white)
![License](https://img.shields.io/badge/License-GPLv3-4CAF50?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)

> **Taller interactivo paso a paso** para capacitar de forma práctica en la implementación completa de **Salesforce Data 360**: desde la ingesta de datos hasta la activación de campañas omnicanal con IA Generativa.

---

### Acceso al Taller

🚀 **Sitio en Vivo:** https://salesforce-data360-workshop-a956d38f5270.herokuapp.com/

---

## Objetivo del Taller

Este workshop tiene como propósito capacitar a consultores, arquitectos y equipos de proyecto en la implementación end-to-end de **Salesforce Data 360**, cubriendo cada capa de la plataforma de forma práctica:

1. **Ingesta** — Conectar fuentes de datos heterogéneas mediante Data Streams.
2. **Transformación** — Limpiar y normalizar datos con Data Transforms.
3. **Unificación** — Construir perfiles únicos de cliente con Identity Resolution.
4. **Enriquecimiento** — Calcular métricas de negocio con Calculated Insights y exponerlas en Salesforce CRM.
5. **Segmentación** — Crear audiencias de alta precisión con el Segment Builder e IA Generativa (Einstein).
6. **Activación** — Enviar segmentos a Marketing Cloud Advanced y orquestar campañas omnicanal.

---

## Caso de Uso: Coral Cloud Resorts

Todos los ejercicios del taller están contextualizados sobre el caso ficticio de **Coral Cloud Resorts**, una cadena hotelera y de experiencias de hospitalidad de lujo que enfrenta el reto común de datos fragmentados.

### El Problema

Coral Cloud Resorts almacena la información de sus huéspedes en múltiples sistemas aislados: reservas en el sistema de gestión hotelera, transacciones en el POS del spa, historial de loyalty en un CRM, soporte en Service Cloud, y comportamiento web en un data lake en S3. Cada sistema usa nomenclaturas distintas (ej. `"Surname"` vs `"LastName"`) y no existe una vista consolidada del huésped. Esto genera fricciones graves como enviar ofertas de "Summer Splash" a clientes con quejas de soporte abiertas.

### La Transformación con Data 360

| Antes | Después |
| :--- | :--- |
| Datos dispersos en 5+ sistemas | Fuente única de verdad en Data 360 |
| Registros duplicados por variaciones de nombre/email | Perfil canónico `Unified Individual` por huésped |
| Métricas de LTV calculadas en Excel de forma manual | Calculated Insights en tiempo real sobre +100M registros |
| Campañas masivas sin segmentación | Audiencias de alta precisión con filtros complejos e IA |
| Brechas entre datos y acción de marketing | Segmentos activados directamente en Marketing Cloud Advanced |

Con **Agentforce** sobre datos unificados, Coral Cloud Resorts también despliega agentes autónomos 24/7: si se detecta una reseña negativa, se dispara un flujo de atención proactiva donde el agente conoce el historial completo, el tier de loyalty y las preferencias del huésped para resolver la situación al instante.

---

## Estructura del Taller — Los 7 Ejercicios

### Mapa de Ejercicios

| # | Ejercicio | Tecnología Principal | Objetivo |
| :---: | :--- | :--- | :--- |
| 0 | Request a Workshop Environment | OrgFarm | Obtener y configurar el entorno de práctica |
| 1 | Unify Data with Data Streams | Data Streams · Data Mapping | Ingerir Cases de Service Cloud y mapear al modelo `Individual` |
| 2 | Manipulate Data with Data Transforms | Data Transforms · DLOs | Limpiar y normalizar números de teléfono en Data Lake Objects |
| 3 | Explore Identity Resolution | Match Rules · Reconciliation Rules · Data Explorer | Unificar perfiles duplicados en un `Unified Individual` |
| 4 | Go Deeper with Calculated Insights | Calculated Insights · Lightning App Builder | Calcular LTV sobre +100M registros y desplegar en vistas de CRM |
| 5 | Segmentation | Segment Builder · Einstein GenAI | Crear audiencias complejas combinando IA y reglas manuales |
| 6 | Activation to Marketing Cloud Advanced | Activations · Marketing Cloud · Flows | Activar segmentos en campañas omnicanal Email + SMS con GenAI |

---

### Ejercicio 0 — Request a Workshop Environment

**Objetivo:** Obtener y configurar el entorno de Salesforce (org) dedicado al taller antes de comenzar los ejercicios prácticos.

**Pasos:**
1. Acceder al formulario en `orgfarm.salesforce.com/signup`.
2. Ingresar el **Event Code** proporcionado por el instructor y tu correo electrónico.
3. Acceder a la org desde la ventana emergente de confirmación.
4. Conservar las credenciales enviadas por email para ingresar en `login.salesforce.com`.

---

### Ejercicio 1 — Unify Data with Data Streams

**Objetivo de negocio:** Los tickets de soporte de Coral Cloud Resorts viven aislados de las interacciones de tienda física, app móvil y e-commerce. Este ejercicio conecta los Cases de Service Cloud a Data 360 para asociar cada reporte de soporte directamente con la identidad única del cliente (`Individual`).

**Lo que construyes:**
- Un **Data Stream** desde Salesforce CRM sobre el objeto `Case`.
- Categorización del stream como **Engagement** (por fecha de creación).
- **Mapping** de campos: `Contact ID → Individual` y `Status → Case Status`.
- Ejecución del primer refresh de ingesta.

**Pasos del ejercicio:**

| Paso | Nombre | Descripción |
| :---: | :--- | :--- |
| 1 | Explorar el Modelo Customer 360 | Navegar al Data Model en Graph View para entender la relación `Individual ↔ Unified Individual` y la arquitectura canónica de objetos. |
| 2 | Ingerir Casos de Soporte desde Service Cloud | Crear un nuevo Data Stream seleccionando Salesforce CRM como fuente y el objeto `Case` con categoría Engagement. |
| 3 | Mapear los Datos al Modelo Customer 360 | Mapear `Contact ID` al objeto `Individual` y el campo `Status` al modelo canónico. Ejecutar Refresh Now para iniciar la ingesta. |

---

### Ejercicio 2 — Manipulate Data with Data Transforms

**Objetivo de negocio:** Los registros de huéspedes de Coral Cloud Resorts contienen números de teléfono mezclados (móvil y casa) con caracteres no numéricos y formatos inconsistentes. Este ejercicio limpia, separa y normaliza esos datos en Data Lake Objects (DLOs) listos para enriquecimiento posterior.

**Lo que construyes:**
- Dos **Data Lake Objects (DLOs)** de destino: `Guest Mobile Phone Numbers` y `Guest Home Phone Numbers`.
- Un **Data Transform** desde el Data Kit que separa los tipos de teléfono, elimina caracteres no numéricos y escribe en los DLOs correspondientes.
- Ejecución del transform con **Run Now**.

**Pasos del ejercicio:**

| Paso | Nombre | Descripción |
| :---: | :--- | :--- |
| 1 | Crear Objetos Data Lake (DLOs) de Destino | Crear los DLOs `Guest Mobile Phone Numbers` y `Guest Home Phone Numbers` desde el Data Kit. |
| 2 | Crear y Ejecutar el Data Transform | Configurar el transform `Format Guest Phone Numbers` desde el canvas, verificar los nodos de transformación y ejecutar Run Now. |

---

### Ejercicio 3 — Explore Identity Resolution

**Objetivo de negocio:** Un mismo huésped puede aparecer como `"Sofia Rodriguez"` en la app y como `"S. Rodriguez"` en el sistema de reservas, con correos similares pero no idénticos. Este ejercicio explora cómo las reglas de coincidencia y reconciliación unifican esos registros dispersos en un único perfil consolidado (`Unified Individual`).

**Lo que construyes:**
- Revisión y comprensión de las **Match Rules** (reglas de coincidencia por nombre, email y teléfono).
- Revisión de las **Reconciliation Rules** (fuente de verdad por campo).
- Uso de **Data Explorer** para validar el "antes y después" de la unificación.

**Pasos del ejercicio:**

| Paso | Nombre | Descripción |
| :---: | :--- | :--- |
| 1 | Revisar las Match Rules | Explorar las reglas configuradas que determinan cuándo dos registros representan a la misma persona. |
| 2 | Revisar las Reconciliation Rules | Comprender qué fuente tiene prioridad para cada campo en el perfil unificado resultante. |
| 3 | Validar con Data Explorer | Consultar el objeto `Unified Individual` en Data Explorer para confirmar que los perfiles duplicados fueron consolidados correctamente. |

---

### Ejercicio 4 — Go Deeper with Calculated Insights

**Objetivo de negocio:** Con los datos unificados bajo `Unified Individual`, Coral Cloud Resorts necesita calcular el **Lifetime Value (LTV)** de cada huésped agregando más de 100 millones de registros de cargos de habitación. Estas métricas deben estar disponibles directamente en las vistas de Contacto de Salesforce CRM para que los representantes de ventas y servicio puedan actuar sobre ellas.

**Lo que construyes:**
- Un **Calculated Insight** de LTV que agrega transacciones a nivel de `Unified Individual`.
- Despliegue de las métricas e historia de actividad unificada en **Lightning App Builder** dentro de la vista de Contactos de Salesforce CRM.

**Pasos del ejercicio:**

| Paso | Nombre | Descripción |
| :---: | :--- | :--- |
| 1 | Explorar Calculated Insights | Revisar los insights preconfigurados (LTV, recencia, categoría preferida) y comprender su lógica de cálculo. |
| 2 | Desplegar Profile Engagements en CRM | Usar Lightning App Builder para incrustar el componente de actividad unificada y métricas del perfil Data 360 en la vista de Contacto. |

---

### Ejercicio 5 — Segmentation

**Objetivo de negocio:** Coral Cloud Resorts ha remodelado su club infantil (**KIDS Camp**) y necesita reconectar con familias que hayan visitado el resort con más de dos niños en el último año. El equipo de marketing debe construir este segmento combinando IA Generativa (Einstein) para la regla inicial y el Segment Builder para agregar filtros avanzados y exclusiones.

**Lo que construyes:**
- Un segmento llamado **"Recent Guests with More Than Two Children"** usando Einstein GenAI como punto de partida.
- Filtros adicionales: actividad web reciente en el período relevante.
- Exclusión de clientes con casos de soporte abiertos.

**Pasos del ejercicio:**

| Paso | Nombre | Descripción |
| :---: | :--- | :--- |
| 1 | Crear Segmento con Einstein GenAI | Usar el prompt de lenguaje natural de Einstein para generar la regla base del segmento `Recent Guests with More Than Two Children`. |
| 2 | Refinar con Segment Builder | Agregar condiciones manuales: filtro por actividad web reciente y exclusión de `Unified Individuals` con cases abiertos. |
| 3 | Publicar el Segmento | Guardar y publicar el segmento para que quede disponible para activación. |

---

### Ejercicio 6 — Activation to Marketing Cloud Advanced

**Objetivo de negocio:** La activación es el proceso mediante el cual una audiencia calculada en Data 360 se materializa y se envía a plataformas de ejecución. En este ejercicio se conecta el segmento **KIDS Camp** creado en el ejercicio anterior a **Marketing Cloud Advanced**, diseñando un flujo omnicanal (Email + SMS) impulsado por IA Generativa.

**Lo que construyes:**
- Una **Activation** del segmento KIDS Camp hacia Marketing Cloud Advanced.
- Una campaña generativa vinculada al flujo **"Kids Camp Off Season Promotion Flow"**.
- Mensajes de Email y SMS generados y personalizados con IA Generativa.
- Revisión del flujo de activación omnicanal completo.

**Pasos del ejercicio:**

| Paso | Nombre | Descripción |
| :---: | :--- | :--- |
| 1 | Crear la Activation Target | Configurar Marketing Cloud Advanced como destino de activación para el segmento. |
| 2 | Seleccionar Segmento y Atributos | Vincular el segmento `Recent Guests with More Than Two Children` y seleccionar los atributos a exportar. |
| 3 | Revisar el Campaign Canvas | Explorar el canvas de la campaña generativa y el flujo `Kids Camp Off Season Promotion Flow`. |
| 4 | Activar con IA Generativa | Generar contenido de Email y SMS personalizado con Einstein GenAI y revisar la activación omnicanal. |

---

## Estructura del Proyecto

```text
salesforce-data360-workshop/
├── index.html                  # Interfaz interactiva principal del taller
├── Procfile                    # Proceso web para despliegue en Heroku (NGINX)
├── static.json                 # Configuración heredada del buildpack estático
├── config/
│   └── nginx.conf.erb          # Configuración NGINX para Heroku
├── assets/
│   ├── css/                    # Estilos y diseño responsivo
│   ├── js/                     # Lógica interactiva (modales, lightbox, navegación)
│   └── img/                    # Capturas de pantalla y recursos visuales
│       ├── ej1/                # Assets del Ejercicio 1 — Data Streams
│       ├── ej2/                # Assets del Ejercicio 2 — Data Transforms
│       ├── ej3/                # Assets del Ejercicio 3 — Identity Resolution
│       ├── ej4/                # Assets del Ejercicio 4 — Calculated Insights
│       ├── ej5/                # Assets del Ejercicio 5 — Segmentación
│       └── ej6/                # Assets del Ejercicio 6 — Activación
└── README.md
```

---

## Ejecución Local

Clona el repositorio y sírvelo con cualquier servidor HTTP estático:

```bash
# 1. Clonar el repositorio
git clone https://github.com/galanteh/salesforce-data360-workshop.git
cd salesforce-data360-workshop

# 2a. Con Python (incluido en macOS/Linux)
python3 -m http.server 8080

# 2b. Con Node.js (npx, sin instalación previa)
npx serve .

# 2c. Con VS Code
# Instalar la extensión "Live Server" y hacer clic en "Go Live"
```

Abre tu navegador en `http://localhost:8080`.

---

## Licencia

Este proyecto está publicado bajo la **GNU General Public License v3.0 (GPLv3)**.

Puedes usar, estudiar, modificar y distribuir este material libremente. Si distribuyes versiones modificadas, debes hacerlo bajo la misma licencia GPLv3, manteniendo el acceso al código fuente y los créditos de autoría. Consulta el archivo [`LICENSE`](LICENSE) para los términos completos.

[![GPLv3](https://img.shields.io/badge/License-GPLv3-4CAF50?style=flat-square)](LICENSE)
