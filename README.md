# Proyecto PIX RPA – Análisis de Productos

## 📌 Descripción del proyecto

Este proyecto implementa una automatización desarrollada en **PIX Robotics** cuyo objetivo es consumir información de productos desde una API externa, procesar y almacenar dichos datos en una base de datos relacional, generar un reporte en formato Excel y realizar la carga del archivo generado en **OneDrive** mediante **Microsoft Graph API**.

El flujo automatizado contempla:

* Consumo de datos en formato JSON.
* Procesamiento e iteración de los productos.
* Validación para evitar duplicados en base de datos.
* Persistencia de la información.
* Generación de un reporte Excel con hojas de detalle y resumen.
* Integración con OneDrive para almacenamiento del reporte.

---

## 🗄️ Creación de la base de datos y tabla

### Base de datos

```sql
CREATE DATABASE IF NOT EXISTS productos_db;
USE productos_db;
```

### Tabla Productos

```sql
CREATE TABLE IF NOT EXISTS Productos (
    id INT PRIMARY KEY,
    title VARCHAR(255),
    price DECIMAL(10,2),
    category VARCHAR(100),
    description TEXT
);
```

La tabla está diseñada para almacenar los productos obtenidos desde la API, utilizando el campo **id** como clave primaria para evitar duplicados.

---

## ▶️ Pasos para la ejecución

1. Clonar o abrir el proyecto en **PIX Robotics**.
2. Configurar las variables de entorno:

   * Credenciales de base de datos.
   * Rutas de carpetas (Reportes, Logs, Evidencias).
   * Credenciales de Microsoft Graph (Client ID, Client Secret, Tenant ID, User ID).
3. Ejecutar el proceso principal, el cual:

   * Consume la API de productos.
   * Inserta los datos en la base de datos validando duplicados.
   * Genera el archivo **Reporte_YYYY-MM-DD.xlsx**.
   * Sube el archivo a OneDrive.
4. Verificar:

   * Registros en la base de datos.
   * Archivo Excel generado localmente.
   * Archivo cargado en OneDrive.

---

## 📦 Requisitos y dependencias

* **PIX Robotics**
* **Base de datos MySQL** (o compatible vía ODBC)
* **Microsoft 365 Business / Enterprise** con licencia activa de **SharePoint Online (OneDrive for Business)**
* **Microsoft Graph API**
* Permisos configurados en Azure:

  * Files.ReadWrite.All
  * Sites.ReadWrite.All
  * User.Read / User.Read.All (según flujo)

---

## ☁️ Integración con OneDrive

La carga del archivo se realiza utilizando **Microsoft Graph API** mediante autenticación OAuth 2.0 (client credentials). El proceso incluye:

* Obtención del token de acceso.
* Lectura del archivo Excel como binario.
* Envío del archivo al endpoint de OneDrive correspondiente al usuario configurado.

> Nota: La ejecución requiere un tenant empresarial con licencia activa; sin esta condición, Microsoft Graph no permite la carga de archivos en OneDrive.

---

## 📝 Enlace del formulario utilizado

Formulario usado para la prueba técnica:

🔗 [https://form.jotform.com/260358594863066](https://form.jotform.com/260358594863066)

---

## 👤 Autor

Proyecto desarrollado por **Michael Sneider Benavides Obando** como parte de una prueba técnica laboral, aplicando buenas prácticas de automatización, integración de servicios y manejo de datos.

---

## ✅ Observaciones finales

La solución fue desarrollada siguiendo buenas prácticas de automatización, modularización de scripts y manejo seguro de credenciales. El proyecto queda listo para ejecutarse en cualquier entorno corporativo que cumpla con los requisitos indicados, sin necesidad de modificaciones adicionales.
