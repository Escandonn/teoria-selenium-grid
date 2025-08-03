# ⚙️ 2. Componentes de Selenium Grid

Selenium Grid se compone de varios elementos que trabajan juntos para distribuir la ejecución de pruebas automatizadas en múltiples entornos. Desde sus versiones iniciales hasta Selenium Grid 4, la arquitectura ha evolucionado, pasando de una estructura centralizada a una basada en microservicios.

A continuación, se describen los componentes clave:


## 🕹️ Hub

El **Hub** es el componente central de Selenium Grid en el modelo clásico (Grid 1, 2 y 3). Su función principal es:

- Recibir solicitudes de pruebas desde clientes (scripts de automatización).
- Determinar qué nodo disponible cumple con los requerimientos (navegador, sistema operativo, versión, etc.).
- Redirigir la prueba al nodo más adecuado.

### Características clave:
- Generalmente corre en una sola máquina.
- Expone un endpoint accesible (por ejemplo, `http://localhost:4444/wd/hub`).
- Centraliza el control y distribución de las pruebas.
- No ejecuta pruebas directamente.

> 🧠 En Grid 4, el rol del Hub tradicional se divide en microservicios más pequeños como el **Router**, **Distributor** y **Session Map**, aunque puede seguir funcionando como "hub" si se usa en modo *classic*.

---

## 🧩 Nodo

Un **Nodo** es un agente que se registra al Hub y tiene la capacidad de ejecutar pruebas en un navegador específico. Puede estar en la misma máquina que el Hub o en otra dentro de la red.

### Características clave:
- Ejecuta instancias de navegadores reales (Chrome, Firefox, Edge, etc.).
- Informa al Hub sobre las **capacidades disponibles**.
- Puede alojar múltiples navegadores o versiones simultáneamente.
- Al ejecutarse remotamente, permite pruebas distribuidas en diferentes SOs.

### Ejemplo de capacidades de un nodo:
```json
{
  "browserName": "chrome",
  "maxInstances": 5,
  "platform": "WINDOWS"
}
🧠 En Grid 4, los nodos ya no usan comandos como `-role node`, sino que se configuran con un archivo JSON o YAML, y forman parte del sistema distribuido completo.

## 🔄 Relación entre Hub y Nodos

La relación entre Hub y Nodos es fundamental para que Selenium Grid funcione correctamente.

### Flujo general:

1. El nodo inicia y se **registra en el hub**, informando qué navegadores y plataformas puede manejar.
2. El cliente (script de prueba) envía una solicitud al hub indicando las **capacidades deseadas**.
3. El hub busca un nodo compatible.
4. Si encuentra uno disponible, **redirige** la prueba a ese nodo.
5. El nodo **ejecuta la prueba** y devuelve los resultados.

### Puntos importantes:

* Si no hay nodos compatibles, la prueba queda en espera o falla.
* El Hub puede manejar múltiples solicitudes concurrentes, distribuyéndolas entre los nodos disponibles.
* Nodos pueden ser dinámicamente agregados o eliminados sin reiniciar el Hub.

---

## 📡 EventBus (Selenium Grid 4)

A partir de Selenium Grid 4, se introduce una arquitectura basada en microservicios, y uno de los componentes principales para la comunicación es el **EventBus**.

### ¿Qué es el EventBus?

Es un canal de mensajería interno que permite que los distintos servicios del Grid se comuniquen entre sí de forma **asíncrona y desacoplada**.

### Servicios que usan EventBus:

* **Router:** recibe solicitudes de prueba desde el cliente.
* **Distributor:** decide a qué nodo enviar la prueba.
* **Session Map:** mantiene el estado de cada sesión activa.
* **Node(s):** ejecutan las pruebas y reportan eventos.

### Características:

* Mejora la escalabilidad y confiabilidad del sistema.
* Usa puertos por defecto (`5557`, `5558`) para transmisión de mensajes.
* Permite separar responsabilidades entre servicios sin crear dependencias rígidas.

> 📌 El uso de EventBus permite desplegar Selenium Grid en clústeres de producción, ya sea con **Docker**, **Kubernetes**, o servicios distribuidos en múltiples regiones.



