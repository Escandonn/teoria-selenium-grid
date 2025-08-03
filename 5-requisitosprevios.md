# 🧰 4. Requisitos Previos

Antes de ejecutar Selenium Grid, es importante asegurarse de que el entorno tenga todos los componentes necesarios instalados. Esto garantiza que los nodos puedan ejecutar correctamente los navegadores y que el hub pueda coordinar las pruebas.


## ☕ Java instalado

Selenium Grid está desarrollado en Java, por lo que es obligatorio tener **Java Runtime Environment (JRE)** o preferiblemente el **Java Development Kit (JDK)** instalado.

### ✅ Requisitos:
- Versión recomendada: **Java 11 o superior**
- Verifica la instalación con:

```bash
java -version
````

> 💡 Asegúrate de que la variable de entorno `JAVA_HOME` esté correctamente configurada para evitar errores al iniciar el servidor.

---

## 📦 Selenium Server (Selenium Grid)

Selenium Grid requiere el archivo ejecutable `selenium-server.jar`, que contiene tanto el Grid como los controladores necesarios para los navegadores.

### 🔽 Descarga:

Puedes descargar el archivo desde el sitio oficial:

👉 [https://www.selenium.dev/downloads/](https://www.selenium.dev/downloads/)

### 💡 Comando básico para iniciar Grid en modo standalone:

```bash
java -jar selenium-server-<version>.jar standalone
```

También puedes iniciarlo en modo `hub` o `node` clásico si lo deseas.

---

## 🌐 Navegadores y Drivers

Para que los nodos puedan ejecutar pruebas en navegadores reales, necesitas instalar los **drivers correspondientes** para cada navegador que vayas a usar.

### Navegadores comunes y sus drivers:

| Navegador       | Driver necesario    | Descarga oficial                                                                                                                               |
| --------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Chrome          | `chromedriver`      | [https://sites.google.com/chromium.org/driver/](https://sites.google.com/chromium.org/driver/)                                                 |
| Firefox         | `geckodriver`       | [https://github.com/mozilla/geckodriver/releases](https://github.com/mozilla/geckodriver/releases)                                             |
| Edge (Chromium) | `msedgedriver`      | [https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/) |
| Safari (macOS)  | Controlador interno | Ya viene incluido con Safari Technology Preview                                                                                                |

### 🔧 Recomendaciones:

* Asegúrate de que los drivers estén en el **PATH del sistema** o especifica su ruta manualmente.
* Las versiones del navegador y del driver deben ser compatibles.
* Puedes automatizar la gestión de drivers con herramientas como:

  * [`WebDriverManager`](https://github.com/bonigarcia/webdrivermanager) (Java)
  * [`selenium-manager`](https://www.selenium.dev/blog/2023/selenium-manager/) (incluido en Selenium 4)

---

## 📁 Otros (opcionales pero útiles)

* 🐍 Python, Node.js, Java o C# si vas a escribir tus scripts de prueba.
* 🧪 Frameworks como **pytest**, **JUnit**, **TestNG**, **Mocha**, etc.
* 🐳 Docker (si planeas ejecutar Grid en contenedores).
* 🔧 Git, Jenkins u otra herramienta de CI/CD si integras pruebas automatizadas en pipelines.



> 📌 **Resumen**:
> Asegúrate de tener **Java**, el **Selenium Server**, los **drivers de navegador** y los **navegadores instalados**. Esto te permitirá iniciar y conectar tanto el Hub como los Nodos correctamente.

