# Arquitectura y Filosofía del Sistema (iOGeminis / Sabiduria-IAH)

## Principles: Sabiduria-IAH
Toda formulación de idea debe crear una respuesta a la toma de cada decisión u opción que como resultado sea en todo momento e instante de **bien común**, para lograr flexibilidad y tolerancia donde pudiese haber llegado a tener un quebranto, siendo la base de todo sistema, código o pensamiento, y obtener un resultado fiable y de confianza total.

## 4.4 Arquitectura Híbrida de Conectividad (Firebase & Backend Intermediario)

Para mitigar riesgos de filtración de credenciales (API Keys) en el cliente móvil, el sistema implementa un flujo de datos segregado:

1. **Autenticación y Telemetría (Firebase):**
   La aplicación cliente (`mx.iogeminis.app`) se comunica directamente con la suite de Firebase utilizando canales TLS 1.3 para la gestión de sesiones de usuario y analíticas operativas genéricas.

2. **Puente de Aislamiento (Backend Propio):**
   Ningún prompt de Inteligencia Artificial se envía directamente desde el dispositivo a los endpoints públicos de Google Cloud. El flujo de texto viaja cifrado desde `mx.iogeminis.app` hacia nuestro servidor backend corporativo.

3. **Invocación Segura:**
   El backend actúa como proxy inverso e intermediario; es el único encargado de custodiar de forma segura las llaves maestras de Vertex AI / Gemini API, inyectar las instrucciones del sistema (*System Instructions*) y realizar la petición final a los servidores de **Google Cloud México, S. de R.L. de C.V.** Este diseño técnico garantiza que el entorno móvil quede libre de secretos criptográficos expuestos y asegura que el procesamiento de datos cumpla con el aislamiento total requerido por el Anexo de Procesamiento de Datos (CDPA).
