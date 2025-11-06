### README.md

# Plantilla Base – RPA 2025

Este proyecto es una **plantilla estándar** para el desarrollo de automatizaciones RPA con UiPath.
Su propósito es ofrecer una base sólida y organizada para iniciar nuevos proyectos, manteniendo coherencia estructural, buenas prácticas y reducción de tiempos de configuración inicial.

---

## Contenido

La plantilla incluye:

* **Estructura de carpetas estandarizada**
  Diseñada para separar lógica de negocio, configuraciones y componentes reutilizables.

* **Archivos recurrentes**

  * `Main.xaml`, `Test.xaml`: flujos principales de ejecución y pruebas.
  * `project.json`: definición de dependencias y metadatos del proyecto.
  * `Jenkinsfile`: configuración para integración continua.

* **Configuraciones base**

  * `config.template`: archivo de variables y parámetros globales.
  * Carpeta `.screenshots/` para evidencia de ejecución automatizada.

* **Regla de uso**
  La plantilla se utiliza **solo como punto de partida**.
  Al crear un nuevo proyecto, se debe eliminar el `.git/` original y configurar un repositorio propio.
  No deben subirse cambios aquí salvo mejoras o actualizaciones de la plantilla en sí.

---

## Estructura de carpetas y archivos

* **BusinessProcess/**
  Carpeta que contiene los procesos de negocio principales, organizados por fases de ejecución que siguen el ciclo completo de una automatización RPA. Cada subcarpeta agrupa workflows con responsabilidades bien definidas para mantener el orden, facilitar el mantenimiento y permitir una rápida comprensión del flujo general.

  * *1.Inicio/* – Incluye las funciones de preparación previas a la ejecución principal. Aquí se realizan acciones como autenticarse en aplicaciones, descargar insumos desde Storage Buckets, obtener información de correo o inicializar configuraciones necesarias.
  * *2.Process/* – Contiene la lógica central del proceso automatizado. En esta sección se definen las reglas específicas, decisiones de negocio y flujos propios del proyecto. Cada .xaml representa una función o bloque funcional exclusivo de la automatización en desarrollo.
  * *3.EndProcess/* – Agrupa los pasos de finalización y cierre ordenado del flujo. Aquí se cierran aplicaciones utilizadas, se generan reportes, se envían correos con resultados y se cargan archivos de salida a Storage Buckets. También pueden incluirse tareas de envío por SFTP, limpieza de recursos o notificaciones de término.
  * *Browser/* – Contiene workflows específicos para interacción con aplicaciones web. Incluye navegación entre URLs, inicio de sesión, descarga de archivos y manipulación de elementos de interfaz. Está diseñado con soporte multibrowser (Chrome, Edge, Firefox) para garantizar compatibilidad y flexibilidad en distintos entornos.

* **Framework/**
  Base de ejecución inspirada en el modelo REFramework de UiPath.
  Incluye workflows esenciales como:

  * `CloseAllApplications.xaml`
  * `GetAppCredentials.xaml`
  * `GetTransactionData.xaml`
  * `InitAllSettings.xaml`
  * `KillAllProcesses.xaml`
  * `RetryCurrentTransaction.xaml`
  * `SelectThrowException.xaml`
  * `SetTransactionStatus.xaml`
  * `TakeScreenshot.xaml`

* **ReusableMethods/**
  Biblioteca de métodos reutilizables, organizada por dominio funcional:

  * **Database/** – Conexión y operaciones con bases de datos.
  * **Datatable/** – Manipulación avanzada de DataTables.
  * **Excel/** – Lectura, escritura y manejo de archivos Excel.
  * **Fechas/** – Utilidades para manejo de fechas y tiempos.
  * **Files&Folders/** – Operaciones sobre archivos y directorios.
  * **Mail/** – Funciones para envío y lectura de correos.
  * **ML_API/** – Llamadas a servicios externos o APIs.
  * **PDF/** – Procesamiento y extracción de contenido de PDFs.
  * **StorageBucket/** – Gestión de datos en Storage Buckets.
  * **System/** – Métodos utilitarios generales.
  * **Text/** – Procesamiento y análisis de texto.

* **.screenshots/**
  Carpeta que almacena automáticamente las capturas generadas por UiPath al identificar o interactuar con elementos de interfaz.
  Estas imágenes sirven como referencia visual para comprender los selectores utilizados y facilitar el mantenimiento o actualización futura de los flujos.

* **Archivos en la raíz del proyecto**

  * `.gitignore`
  * `Jenkinsfile` – Pipeline de integración continua.
  * `Main.xaml` – Flujo principal de automatización.
  * `Main.xaml.json` – Configuración del flujo principal.
  * `Test.xaml` – Flujo de pruebas.
  * `project.json` – Metadatos del proyecto UiPath.

---

## Instrucciones de uso

1. Clonar o descargar esta plantilla.
2. Eliminar la carpeta `.git/` y crear un nuevo repositorio para el proyecto.
3. Actualizar `project.json` con el nombre y detalles del nuevo proyecto.
4. Implementar la lógica del proceso dentro de `BusinessProcess/`.
5. Utilizar los componentes disponibles en `ReusableMethods/` para maximizar la reutilización.
6. Mantener la estructura limpia y coherente con el estándar base.

---

## Estructura_Plantilla
  Carpeta donde el robot gestiona todos los recursos de ejecución. Aquí se almacenan los **insumos**, **resultados** y **evidencias** generadas durante el proceso. Su estructura está pensada para mantener trazabilidad completa y facilitar la depuración o auditoría posterior.  

  * Contiene subcarpetas para **screenshots**, **videos**, **inputs** y **outputs**, donde se registran automáticamente las capturas de pantalla, grabaciones y archivos procesados por el flujo.  
  * Incluye el archivo **`config.xlsx`**, que centraliza los **assets** y **parámetros globales** utilizados por el robot. Este archivo actúa como el punto de control principal del flujo, definiendo credenciales, rutas y configuraciones reutilizables.  
  * Además, incorpora el **`dynamicconfig.xlsx`**, diseñado para controlar configuraciones dinámicas relacionadas con archivos externos.  
    En este archivo se define la estructura y comportamiento esperado de cada insumo, por ejemplo:  
    - Nombre del archivo de entrada (por ejemplo, `excelReporteInput.xlsx`).  
    - Hojas que contiene (`"x"`, `"y"`, `"F"`).  
    - Rango o celda inicial de lectura (`A10`).  
    - Columnas de filtrado o claves (`colname1`, etc.).  

  En conjunto, estos componentes permiten que el robot ejecute flujos de forma parametrizada y adaptable, sin necesidad de modificar directamente los workflows en UiPath.

  Pasos para su uso:
  1. Cambiar "Estructura_Plantilla" por el nombre correspondiente para el flujo automatizado a generar
  2. Actualizar datos clave en Config.xlsx (el nombre de la carpeta)
  3. Actualizar datos clave en el Main.xaml para que los nombres coincidan.
  4. Actualizar, añadir, eliminar assets según las necesidades.

---

## Autor y contacto

**Autor:** Jorge A. Falcón
📫 [Correo](mailto:contacto.jf.dollhouse327@passinbox.com)
🌐 [Telegram](https://t.me/jfespanolito)
💻 [GitHub](https://github.com/JFEspanolito)
🔗 [LinkedIn](https://www.linkedin.com/in/jfespanolito/)
🐦 [Twitter](https://twitter.com/JFEspanolito)
🎓 [Platzi](https://platzi.com/@jfespanolito/)