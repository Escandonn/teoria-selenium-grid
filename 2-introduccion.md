

# 📘 1. Introducción a Selenium Grid

## 🤖 ¿Qué es Selenium Grid?

**Selenium Grid** es una herramienta de pruebas distribuidas que permite ejecutar pruebas automatizadas en múltiples navegadores, sistemas operativos y máquinas al mismo tiempo. Forma parte del ecosistema de **Selenium**, un conjunto de herramientas para automatización de navegadores web.

En lugar de ejecutar todas las pruebas en un solo equipo (lo que puede ser lento y limitado), Selenium Grid permite **distribuir la ejecución** a través de una red de máquinas, lo que se conoce como una **arquitectura cliente-servidor**:

- El **Hub** actúa como el punto central que recibe las pruebas.
- Los **Nodos** son las máquinas que ejecutan esas pruebas.

Esto permite escalar horizontalmente y realizar **pruebas paralelas** en diferentes entornos de manera eficiente.


## 🎯 Casos de uso y ventajas

### 🧪 Casos de uso comunes:
- Ejecutar pruebas en **diferentes versiones de navegadores** (Chrome, Firefox, Edge, etc.).
- Validar aplicaciones web en **distintos sistemas operativos** (Windows, macOS, Linux).
- **Acelerar la ejecución de pruebas** ejecutando casos en paralelo.
- Integrar pruebas en pipelines **CI/CD (Integración continua)**.
- Probar en dispositivos físicos o virtuales conectados a nodos remotos.

### ✅ Ventajas de usar Selenium Grid:
- **Escalabilidad**: Agregar más nodos según la demanda sin cambiar el hub.
- **Ahorro de tiempo**: Pruebas en paralelo reducen el tiempo total de ejecución.
- **Flexibilidad**: Cada nodo puede estar configurado con distintos navegadores o resoluciones.
- **Centralización**: El hub centraliza la asignación y monitoreo de las pruebas.
- **Compatibilidad**: Funciona con múltiples lenguajes de programación (Java, Python, C#, JavaScript).


## 🧱 Arquitectura general

La arquitectura de Selenium Grid está basada en el patrón **Hub-Nodo**. Desde **Selenium Grid 4**, también se introdujo una arquitectura más moderna basada en **microservicios** con componentes como el **EventBus**, **Router**, **SessionMap**, entre otros. Aquí veremos primero la versión clásica:

### 🕹️ Hub
- Es el servidor principal.
- Recibe las peticiones de ejecución de pruebas (por ejemplo, desde un script en Python o Java).
- Asigna la prueba al nodo más adecuado según las capacidades solicitadas.

### 🧩 Nodo
- Es una máquina (física o virtual) que ejecuta los navegadores reales.
- Puede tener uno o más navegadores disponibles.
- Cada nodo se registra en el hub al iniciar.

### 🔁 Flujo básico
1. El usuario (cliente) ejecuta una prueba apuntando al **hub**.
2. El hub analiza las **deseadas capacidades** (por ejemplo, navegador Chrome en Linux).
3. El hub redirige la prueba a un **nodo compatible**.
4. El nodo abre el navegador y ejecuta la prueba.

Perfecto, aquí tienes todo el contenido completo del punto **1. Introducción a Selenium Grid** en **formato `.md` válido**, con buena estructura, emojis y listas claras. Puedes copiarlo directamente a un archivo llamado `01-introduccion-selenium-grid.md`.



## 🧱 Arquitectura general

Selenium Grid se basa en el patrón **Hub-Nodo**.

### 🕹️ Hub
- Es el servidor central que recibe las pruebas desde el cliente (por ejemplo, un script de prueba en Python).
- Decide a qué nodo enviar la prueba según las capacidades requeridas (SO, navegador, versión).

### 🧩 Nodo
- Es una máquina (física o virtual) que ejecuta las pruebas en un navegador real.
- Se registra ante el hub y le informa qué capacidades ofrece.



* El script apunta al hub (por ejemplo: `http://localhost:4444/wd/hub`).
* El hub distribuye la ejecución según disponibilidad y requisitos.
* Los nodos ejecutan la prueba con el navegador indicado.



> 📌 **Nota Importante:**
> Desde **Selenium Grid 4**, la arquitectura se modernizó. Ahora puede ejecutarse en **tres modos**, según el contexto y el nivel de escalabilidad requerido.

### 🔧 Modos de ejecución en Selenium Grid 4

| Modo             | Descripción                                                                              |
| ---------------- | ---------------------------------------------------------------------------------------- |
| 🧪 `Standalone`  | Todo en uno. Ideal para desarrollo local y pruebas simples.                              |
| 🧱 `Classic`     | Arquitectura tradicional Hub-Nodos. Útil para configuraciones manuales.                  |
| ☸️ `Distributed` | Basado en microservicios. Se recomienda usar Docker o Kubernetes. Ideal para producción. |
