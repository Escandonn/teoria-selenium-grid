# 📈 3. Versiones de Selenium Grid

Selenium Grid ha evolucionado significativamente desde su primera versión, adaptándose a las necesidades crecientes de pruebas automatizadas a gran escala. A continuación se presenta una visión general de las distintas versiones y los cambios más relevantes.

---

## 📜 Evolución (Grid 1, 2, 3, 4)

### 🟠 **Selenium Grid 1 (2008)**
- Basado en *Selenium RC*.
- Arquitectura muy simple.
- Solo podía ejecutar pruebas escritas con Selenium RC.
- Limitada compatibilidad con navegadores modernos.
- **Obsoleto actualmente.**

### 🟡 **Selenium Grid 2 (2011)**
- Introduce la arquitectura **Hub-Nodo** como base del sistema.
- Compatible con **WebDriver**, mejorando el control de navegadores.
- Permite ejecutar pruebas en paralelo en múltiples máquinas.
- Utiliza la **línea de comandos** para lanzar nodos y hub.
- Alta adopción en entornos locales y pequeños pipelines de CI.

### 🟢 **Selenium Grid 3 (2016)**
- Se mejora el soporte para pruebas distribuidas.
- Mejor integración con herramientas de CI (Jenkins, GitLab, etc.).
- Capacidad para configurar **capabilities** más detalladas.
- Soporte para múltiples navegadores y versiones por nodo.
- Sigue siendo ampliamente utilizado en entornos legacy.
- Problemas de escalabilidad y manejo de sesiones bajo alta carga.

### 🔵 **Selenium Grid 4 (2021)**
- Rediseño completo de la arquitectura.
- Basado en **microservicios** y comunicación interna con **EventBus**.
- Soporte nativo para **Docker**, **Kubernetes** y despliegue en la nube.
- Nuevos modos de ejecución: *Standalone*, *Classic* y *Distributed*.
- Interfaz web moderna para monitoreo en tiempo real.
- Comunicación segura por HTTPS y soporte para autenticación.

---

## ✨ Novedades en Selenium Grid 4

Selenium Grid 4 representa una evolución completa, pensada para entornos modernos de pruebas en la nube, CI/CD y arquitecturas distribuidas.

### 🔧 Arquitectura modular
- Cada componente (Router, Distributor, SessionMap, EventBus, Node) es independiente.
- Mayor tolerancia a fallos y mejor distribución de carga.
- Se puede desplegar como **microservicios** o contenedores separados.

### 🧪 Nuevos modos de ejecución

| Modo            | Descripción                                                                 |
|-----------------|------------------------------------------------------------------------------|
| 🧪 `Standalone`   | Todo en uno. Ideal para desarrollo local o entornos simples.                |
| 🧱 `Classic`      | Reproduce el patrón Hub-Nodos clásico. Útil en entornos conocidos.          |
| ☸️ `Distributed`  | Despliegue distribuido. Ideal para escalabilidad horizontal y CI/CD.       |

### 🌐 Compatibilidad mejorada
- Soporte oficial para los navegadores modernos (Chrome, Firefox, Edge, Safari).
- Integración más estable con navegadores mediante WebDriver actualizados.

### 🖥️ UI de monitoreo integrada
- Panel gráfico para ver:
  - Nodos activos
  - Sesiones en ejecución
  - Estadísticas del sistema
- Accesible desde navegador (`http://localhost:4444/ui`)

### 🔒 Seguridad mejorada
- Comunicación cifrada mediante **TLS/SSL**.
- Configuración de autenticación básica y tokens de acceso.
- Mejor manejo de sesiones activas.



> 🧠 **Resumen**:  
> Selenium Grid 4 permite escalar, monitorear y administrar pruebas distribuidas de forma profesional, alineándose con entornos de despliegue modernos como Docker, CI/CD y la nube.

