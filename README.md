# 👁️ Desafío Técnico: Visión por Computadora e Inteligencia Artificial

Este repositorio contiene las soluciones implementadas para el desafío técnico de Computer Vision. El proyecto demuestra capacidades en **análisis de actividad humana (HAR)**, **streaming RTSP en tiempo real**, **arquitecturas multi-cámara paralelas** y **sistemas multi-agente**.

---

## 🛠️ Tecnologías Utilizadas

* **Lenguaje:** Python 3.10+
* **Visión por Computadora:** OpenCV, Ultralytics YOLOv8 (Pose & Detection)
* **Cloud & Concurrencia:** AWS Boto3, Threading, Python Multiprocessing
* **Formatos:** JSON (Telemetría), MP4/AVI (Video procesado)

## 🚀 Instalación y Configuración

1.  **Clonar el repositorio:**
    ```bash
    git clone [https://github.com/ManuJ05/desafio-vision.git](https://github.com/ManuJ05/desafio-vision.git)
    cd desafio-vision
    ```

2.  **Instalar dependencias:**
    ```bash
    pip install opencv-python ultralytics boto3 numpy
    ```

3.  **Configuración de Video:**
    > **Nota Importante:** Por buenas prácticas, este repositorio no incluye archivos de video pesados.
    
    Para probar los scripts, por favor coloca un archivo llamado `video_entrada.mp4` en la carpeta raíz del proyecto. Si el script no encuentra el archivo, intentará activar tu **Webcam (0)** automáticamente.

---

## 📂 Descripción de los Ejercicios

### 1. Análisis HAR y Telemetría Cloud (`ejercicio1.py`)
Sistema de monitoreo biomecánico utilizando **Pose Estimation**.
* **Funcionalidad:** Detecta personas, calcula el ángulo del codo en tiempo real y determina el estado de actividad (Activo/Estático).
* **Arquitectura:** Implementa subida asíncrona a **AWS S3** (simulado o real) usando hilos en segundo plano para no bloquear el procesamiento de video.

### 2. Streaming RTSP sin Latencia (`ejercicio2.py`)
Solución al problema de latencia (buffer lag) en streams de red.
* **Funcionalidad:** Implementa el patrón **Productor-Consumidor**. Un hilo dedicado captura frames y descarta los antiguos, asegurando que la inferencia siempre se realice sobre la imagen más reciente ("Near Real-Time").
* **Salida:** Genera un video `.mp4` y un log `.json` de detecciones.

### 3. Sistema Multi-Cámara Paralelo (`ejercicio3.py`)
Sistema de vigilancia para múltiples fuentes simultáneas.
* **Arquitectura:** Utiliza **Multiprocessing** (procesos aislados) en lugar de Threads.
* **Ventaja:** Permite ejecutar 3 instancias independientes de YOLOv8 aprovechando múltiples núcleos de la CPU, evitando el cuello de botella del GIL de Python.
* **Resultado:** Cada cámara graba su propio video y logs de forma independiente, visualizados en un monitor unificado.

### 4. Agentes Inteligentes (`ejercicio4.py`)
Simulación de una arquitectura **Multi-Agente** para seguridad industrial.
* **Agente Vision:** Percibe el entorno (simulado) y genera datos estructurados.
* **Agente Seguridad:** Analiza los datos buscando violaciones de normas (ej. falta de EPP - Equipo de Protección Personal) y emite alertas críticas.

---

## 📄 Estructura de Archivos

```text
├── ejercicio1.py         # Script HAR + AWS S3
├── ejercicio2.py         # Script RTSP Anti-Lag
├── ejercicio3.py         # Script Multi-Cámara (Multiprocessing)
├── ejercicio4.py         # Script Lógica de Agentes
├── .gitignore            # Configuración de exclusión de archivos
└── README.md             # Documentación del proyecto
