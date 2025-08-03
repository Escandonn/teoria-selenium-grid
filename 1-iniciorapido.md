# ✨ Guía Rápida para Comenzar con Selenium Grid

## 🌐 Introducción

Selenium Grid permite ejecutar pruebas automatizadas en múltiples navegadores, sistemas operativos y máquinas de forma paralela. Esta guía te ayudará a comenzar de forma rápida usando diferentes modos: **Standalone**, **Hub & Node**, y **Distribuido**.

---

## 📅 Requisitos Previos

* Java 11 o superior instalado
* Navegador(es) instalados
* Driver(s) de navegador instalados (opcional si usas `--selenium-manager true`)
* El ejecutable de Java debe estar en el `PATH`
* Descargar el archivo `.jar` del [Selenium Server](https://www.selenium.dev/downloads/)

---

## ⚡ Inicio Rápido (Modo Standalone)

1. Ejecuta el siguiente comando:

```bash
java -jar selenium-server-<version>.jar standalone
```

2. Apunta tus pruebas WebDriver a: `http://localhost:4444`

3. (Opcional) Abre tu navegador en `http://localhost:4444` para ver el estado de la Grid.

---

## 🛠️ Modos de Ejecución de Selenium Grid

### 1. Modo Standalone

Todo en un solo proceso. Ideal para pruebas locales, CI/CD, o debug.

```bash
java -jar selenium-server-<version>.jar standalone
```

### 2. Modo Hub & Node

#### Hub

```bash
java -jar selenium-server-<version>.jar hub
```

#### Node (misma máquina que Hub)

```bash
java -jar selenium-server-<version>.jar node
```

#### Múltiples Nodes en la misma máquina

```bash
java -jar selenium-server-<version>.jar node --port 5555
java -jar selenium-server-<version>.jar node --port 6666
```

#### Node en máquina diferente al Hub

```bash
java -jar selenium-server-<version>.jar node --hub http://<hub-ip>:4444
```

Si el Hub no usa puertos por defecto:

```bash
java -jar selenium-server-<version>.jar hub \
  --publish-events tcp://<hub-ip>:8886 \
  --subscribe-events tcp://<hub-ip>:8887 \
  --port 8888

java -jar selenium-server-<version>.jar node \
  --publish-events tcp://<hub-ip>:8886 \
  --subscribe-events tcp://<hub-ip>:8887
```

### 3. Modo Distribuido (Componentes separados)

* **Event Bus**

```bash
java -jar selenium-server-<version>.jar event-bus \
  --publish-events tcp://<event-bus-ip>:4442 \
  --subscribe-events tcp://<event-bus-ip>:4443 \
  --port 5557
```

* **New Session Queue**

```bash
java -jar selenium-server-<version>.jar sessionqueue --port 5559
```

* **Session Map**

```bash
java -jar selenium-server-<version>.jar sessions \
  --publish-events tcp://<event-bus-ip>:4442 \
  --subscribe-events tcp://<event-bus-ip>:4443 \
  --port 5556
```

* **Distributor**

```bash
java -jar selenium-server-<version>.jar distributor \
  --publish-events tcp://<event-bus-ip>:4442 \
  --subscribe-events tcp://<event-bus-ip>:4443 \
  --sessions http://<sessions-ip>:5556 \
  --sessionqueue http://<queue-ip>:5559 \
  --port 5553 --bind-bus false
```

* **Router**

```bash
java -jar selenium-server-<version>.jar router \
  --sessions http://<sessions-ip>:5556 \
  --distributor http://<distributor-ip>:5553 \
  --sessionqueue http://<queue-ip>:5559 \
  --port 4444
```

* **Node**

```bash
java -jar selenium-server-<version>.jar node \
  --publish-events tcp://<event-bus-ip>:4442 \
  --subscribe-events tcp://<event-bus-ip>:4443
```

---

## 📈 Consultar el estado de la Grid

* UI Web: `http://localhost:4444`
* API REST: `http://localhost:4444/status`
* GraphQL

---

## 💪 Configurar Metadata en tus pruebas (Java)

```java
ChromeOptions chromeOptions = new ChromeOptions();
chromeOptions.setCapability("browserVersion", "100");
chromeOptions.setCapability("platformName", "Windows");
chromeOptions.setCapability("se:name", "Mi prueba simple");
chromeOptions.setCapability("se:sampleMetadata", "valor ejemplo");

WebDriver driver = new RemoteWebDriver(new URL("http://localhost:4444"), chromeOptions);
driver.get("http://www.google.com");
driver.quit();
```

---

## 🚀 Cambiar a cliente HTTP de Java 11

Descarga `selenium-http-jdk-client-<version>.jar` y luego:

```bash
java -Dwebdriver.http.factory=jdk-http-client \
  -jar selenium-server-<version>.jar \
  --ext selenium-http-jdk-client-<version>.jar standalone
```

O usando Coursier:

```bash
java -Dwebdriver.http.factory=jdk-http-client \
  -jar selenium-server-<version>.jar \
  --ext $(coursier fetch -p org.seleniumhq.selenium:selenium-http-jdk-client:<version>) standalone
```

---

## 📊 Tamaño recomendado del Grid

| Tamaño      | Descripción                                    |
| ----------- | ---------------------------------------------- |
| **Pequeño** | Hasta 5 Nodes                                  |
| **Mediano** | 6 a 60 Nodes                                   |
| **Grande**  | 60 a 100+ Nodes (modo Distribuido recomendado) |

* 1 CPU + 1GB RAM por navegador (recomendado)
* Mejor muchos Nodes pequeños que uno grande (aislamiento)

---

## ⚠️ Seguridad

Protege la Grid del acceso externo con reglas de firewall adecuadas. Una Grid abierta puede ser mal utilizada para:

* Acceder a aplicaciones internas
* Ejecutar binarios maliciosos
* Leer archivos internos

Consulta: "Don’t Leave your Grid Wide Open" en Detectify Labs.

---

## 📖 Recursos Adicionales

* [Componentes](https://www.selenium.dev/documentation/grid/components/)
* [Configuración avanzada](https://www.selenium.dev/documentation/grid/configuration/)
* [Arquitectura](https://www.selenium.dev/documentation/grid/architecture/)
* [Funciones avanzadas](https://www.selenium.dev/documentation/grid/advanced_features/)
