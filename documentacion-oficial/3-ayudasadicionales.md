
# 🛠️ **Guía de Configuración en Selenium Grid 4 – Comandos de Ayuda**

Selenium Grid 4 incluye una serie de **comandos integrados de ayuda** que permiten acceder a la información más actualizada sobre la configuración de Grid. Esta es la forma más fiable y sencilla de conocer las opciones disponibles, especialmente si la documentación oficial aún no está actualizada.

---

## 📘 **1. Comando `info`**

El comando `info` proporciona **documentación detallada** sobre varios aspectos clave de Selenium Grid:

| Tema                     | Descripción                                                              |
| ------------------------ | ------------------------------------------------------------------------ |
| **Configuring Selenium** | Explicación general de cómo configurar Grid.                             |
| **Security**             | Guía para establecer comunicación segura y registro de nodos.            |
| **Session Map setup**    | Opciones para almacenar la información de sesiones (local, Redis, JDBC). |
| **Tracing**              | Configuración para rastreo y visualización con OpenTelemetry y Jaeger.   |

🔧 **Ejemplo general de uso:**

```bash
java -jar selenium-server-<versión>.jar info config
```

---

## 🔐 **2. Seguridad (Security)**

Para conocer cómo establecer una **comunicación segura** entre los componentes del Grid, incluyendo autenticación de nodos, ejecuta:

```bash
java -jar selenium-server-<versión>.jar info security
```

---

## 💾 **3. Configuración del Session Map**

Por defecto, Selenium Grid utiliza un **Session Map local**, pero también puede usar opciones avanzadas como:

* **Redis**
* **Bases de datos SQL vía JDBC**

🧠 Para obtener instrucciones sobre cómo configurar estas opciones:

```bash
java -jar selenium-server-<versión>.jar info sessionmap
```

---

## 📊 **4. Trazabilidad y OpenTelemetry**

El rastreo está **habilitado por defecto**. Puedes exportar trazas para visualizarlas en herramientas como **Jaeger**.

📈 Para obtener instrucciones:

```bash
java -jar selenium-server-<versión>.jar info tracing
```

---

## 📋 **5. Mostrar todos los comandos disponibles**

Para listar **todas las opciones de configuración disponibles** (con sus descripciones):

```bash
java -jar selenium-server-<versión>.jar --config-help
```

---

## ⚙️ **6. Ayuda específica por componente**

Cada **rol o componente** de Selenium Grid tiene su propio conjunto de configuraciones. Puedes obtener ayuda específica con el parámetro `--help`.

### 🧍 Standalone (modo todo en uno)

```bash
java -jar selenium-server-<versión>.jar standalone --help
```

### 🧠 Hub (modo tradicional)

```bash
java -jar selenium-server-<versión>.jar hub --help
```

### 📤 Sessions (gestor de sesiones)

```bash
java -jar selenium-server-<versión>.jar sessions --help
```

### 📦 New Session Queue (cola de nuevas sesiones)

```bash
java -jar selenium-server-<versión>.jar sessionqueue --help
```

### 🧭 Distributor (distribuidor de sesiones)

```bash
java -jar selenium-server-<versión>.jar distributor --help
```

### 🌐 Router (encaminador de solicitudes)

```bash
java -jar selenium-server-<versión>.jar router --help
```

### 🧪 Node (ejecutor de pruebas)

```bash
java -jar selenium-server-<versión>.jar node --help
```

---

## ✅ **Resumen**

| Función                        | Comando                                             |
| ------------------------------ | --------------------------------------------------- |
| Configuración general          | `java -jar selenium-server.jar info config`         |
| Seguridad                      | `java -jar selenium-server.jar info security`       |
| Session Map avanzado           | `java -jar selenium-server.jar info sessionmap`     |
| Trazabilidad con Jaeger        | `java -jar selenium-server.jar info tracing`        |
| Todos los comandos disponibles | `java -jar selenium-server.jar --config-help`       |
| Ayuda por componente           | `java -jar selenium-server.jar <componente> --help` |

