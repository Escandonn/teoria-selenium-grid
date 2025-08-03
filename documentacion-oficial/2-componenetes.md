

# 🧩 **Componentes de Selenium Grid 4 - Guía Completa**

Selenium Grid 4 ha sido reescrito desde cero para adaptarse al entorno moderno de desarrollo: computación en la nube, contenedores y escalabilidad distribuida. Cada función clave del Grid ahora es manejada por componentes independientes, que se comunican entre sí para ofrecer un alto rendimiento y control.



## 🔗 **1. Router**

El **Router** es la **puerta de entrada principal** al Grid. Su función es recibir todas las solicitudes externas (normalmente desde un cliente como Selenium WebDriver) y redirigirlas adecuadamente:

* Si se trata de una **nueva solicitud de sesión**, el Router la envía a la **New Session Queue**.
* Si la solicitud pertenece a una **sesión ya existente**, el Router consulta el **Session Map** para encontrar en qué **Node** está corriendo esa sesión, y luego reenvía directamente la solicitud al Node correspondiente.

Además, el Router **balancea la carga** distribuyendo las solicitudes para evitar sobrecargar componentes innecesarios.


## 🤖 **2. Distributor**

El **Distributor** cumple dos roles esenciales:

### 📌 a) Registro y monitoreo de Nodes

* Cada **Node** se registra en el Distributor a través del **Event Bus**.
* El Distributor valida que el Node exista (enviando una solicitud HTTP).
* Si responde correctamente, se registra el Node y sus **capacidades** (por ejemplo, navegadores disponibles, sistema operativo, etc.) dentro de un modelo llamado **GridModel**.

### 📌 b) Procesamiento de nuevas sesiones

* Consulta periódicamente la **New Session Queue** para detectar nuevas solicitudes.
* Busca un **Node adecuado** donde pueda crear la sesión.
* Si la sesión se crea con éxito, el Distributor guarda en el **Session Map** el **ID de la sesión** y el **Node** asignado.

---

## 🗺️ **3. Session Map**

El **Session Map** es una especie de “mapa” o base de datos interna que guarda el vínculo entre:

* El **ID de la sesión**
* El **Node** donde esa sesión se está ejecutando

Esto permite al Router redirigir correctamente futuras solicitudes a la máquina correspondiente.

---

## 🧾 **4. New Session Queue**

La **New Session Queue** es una **cola FIFO** (primero en entrar, primero en salir) que gestiona todas las solicitudes para **nuevas sesiones**:

* Las solicitudes se agregan aquí por el **Router**
* Tiene parámetros configurables como:

  * **Timeout** (tiempo máximo en la cola)
  * **Intervalo de reintento**

El **Distributor** revisa esta cola continuamente:

1. Si encuentra un **Node libre y compatible**, intenta crear la sesión.
2. Si **todos los slots están ocupados**, reintenta o deja la solicitud en la cola.
3. Si expira el tiempo de espera, la solicitud es rechazada.

Una vez creada la sesión:

* La información fluye: **Distributor → New Session Queue → Router → Cliente**

---

## 🧩 **5. Node**

Un **Node** es una máquina (física o virtual) que ejecuta las pruebas en navegadores específicos. Cada Grid puede tener múltiples Nodes.

### Características:

* Se **registra automáticamente** al Distributor usando el **Event Bus**
* Detecta los **drivers disponibles** (ChromeDriver, GeckoDriver, etc.)
* Crea **slots** para cada navegador en función de los núcleos de CPU
* Puede correr sesiones en **contenedores Docker** o por medio de configuración específica

⚠️ Un Node solo ejecuta comandos; no toma decisiones ni coordina.
Puede ser Windows, Linux o macOS (incluso combinados en el mismo Grid).

---

## 🔁 **6. Event Bus**

El **Event Bus** es el **canal de comunicación interno** entre todos los componentes:

* Nodes
* Distributor
* Session Map
* New Session Queue

📡 Transmite eventos y mensajes, evitando así llamadas HTTP innecesarias.
Debe ser el **primer componente** que se inicia en un Grid distribuido.

---

## 🧪 **¿Cómo usar estos componentes?**

Cada uno de estos módulos puede ejecutarse en su propio contenedor o máquina, permitiendo escalabilidad horizontal. Para aprender a montar todo el sistema, dirígete a la sección **"Primeros pasos con Selenium Grid 4"**, donde podrás ver ejemplos de despliegue local, en red y en la nube.

