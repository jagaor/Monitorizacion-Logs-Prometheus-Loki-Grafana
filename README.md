# Monitorización y Registro Centralizado de Logs

## 📝 Descripción General
Este proyecto forma parte del módulo de "Bastionado de Redes" y se centra en la observabilidad de la infraestructura. El objetivo es desplegar un entorno de monitorización integral que permita recopilar, almacenar y visualizar tanto métricas de rendimiento (CPU, RAM, red) como registros de eventos (logs) en tiempo real, facilitando la detección temprana de anomalías y la auditoría de sistemas.

## 🎯 Objetivos del Proyecto
* Desplegar una topología de red virtualizada utilizando GNS3 con nodos basados en contenedores Docker (Ubuntu).
* Implementar **Prometheus** como motor principal para la recolección y almacenamiento de métricas de series temporales.
* Configurar **Grafana Loki** para la agregación y centralización de logs, optimizando el almacenamiento sin indexar el texto completo.
* Utilizar agentes de recolección en los nodos finales (como **Node Exporter** para métricas y **Promtail** para logs) para enviar la telemetría al servidor central.
* Diseñar dashboards interactivos en **Grafana** para visualizar el estado de salud de la infraestructura y cruzar datos de métricas con registros del sistema.

## 🛠️ Tecnologías y Herramientas
* **Simulación y Entorno**: GNS3, VirtualBox / VMware.
* **Sistemas Operativos**: Ubuntu Server, Ubuntu Docker Guests.
* **Stack de Monitorización (Métricas)**: Prometheus, Node Exporter.
* **Stack de Logs**: Grafana Loki, Promtail.
* **Visualización y Alertas**: Grafana.

## ⚙️ Detalles de Implementación Destacados
* **Arquitectura Cliente-Servidor**: Se configuró un nodo central (Servidor de Monitorización) alojando las bases de datos de Prometheus y Loki junto con el panel de Grafana. Los nodos "víctima" o clientes ejecutan de forma silenciosa los agentes `node_exporter` y `promtail`.
* **Recolección de Logs**: A través de `promtail`, se monitorizaron los archivos de registro locales (como `/var/log/syslog` y logs de contenedores), enviando flujos continuos a Loki etiquetados por host y servicio para facilitar su filtrado posterior (usando LogQL).
* **Consumo de Recursos**: Se comprobó que los agentes de extracción en los nodos clientes tienen un impacto mínimo en el sistema, visualizando sus procesos activos mediante comandos nativos (`ps aux`).
* **Visualización en Grafana**: Se conectaron las fuentes de datos (Data Sources) de Prometheus y Loki al panel de Grafana. Esto permitió la creación de vistas divididas donde se puede correlacionar un pico de uso de CPU (Prometheus) con los errores del sistema registrados en ese mismo instante exacto (Loki).

## 📄 Documentación Completa
Para consultar la configuración exacta de los archivos `.yaml` (Prometheus, Promtail, Loki), las topologías de red en GNS3 y las capturas de los paneles de Grafana en funcionamiento, revisa la memoria técnica del proyecto:

👉 [Enlace al Informe Técnico en Google Drive](https://docs.google.com/document/d/1_CdwPvnznLybRXvHaa6LeLy2zZluErXbqaWh2UpKk2I/edit?usp=sharing)

## ⚠️ Aviso Legal / Ética
*La monitorización de sistemas y recolección de logs es una tarea crítica para los equipos de Blue Team y administradores de sistemas. Este entorno se ha desplegado en un laboratorio aislado para comprender los flujos de telemetría de forma segura y respetando la privacidad.*
