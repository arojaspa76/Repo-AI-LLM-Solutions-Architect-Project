# Plantilla oficial del Proyecto Final  
**Curso:** Proyectos reales de Ingeniería de Datos con Python  
**Nivel:** Maestría (alto rigor técnico)  
**Proveedor principal:** Google Cloud Platform (GCP)

---

## 1. Enfoque pedagógico y viabilidad multi-cloud

Este proyecto final está diseñado bajo un enfoque **vendor-agnostic**, con una **implementación de referencia en GCP**, y equivalencias conceptuales con AWS y Azure.

Principios clave:
- Una sola arquitectura lógica obligatoria
- Un solo pipeline en Python
- Adaptadores por proveedor cloud
- Configuración externa (no lógica acoplada a la nube)

El estudiante implementa **una nube**, pero demuestra capacidad de razonamiento **multi-cloud**.

---

## 2. Arquitectura oficial obligatoria del proyecto

### 2.1 Arquitectura lógica

Todo proyecto final debe implementar el siguiente flujo:

Sources → Extract → Raw (Bronze) → Transform → Curated (Silver) → Serving (Gold)

Requisitos mínimos:
- Pipeline batch o incremental
- Integración de múltiples fuentes
- Separación clara de responsabilidades
- Almacenamiento final en la nube
- Preparación para automatización

---

### 2.2 Arquitectura física (equivalencias por nube)

| Capa | AWS | GCP | Azure |
|---|---|---|---|
| Ingesta | Lambda / ECS | Cloud Run / Functions | Azure Functions |
| Raw (Bronze) | S3 | GCS | ADLS Gen2 |
| Transform | Glue / EMR | Dataflow / Dataproc | Synapse / Databricks |
| Curated (Silver) | S3 Parquet | GCS Parquet | ADLS Parquet |
| Serving (Gold) | Athena / Redshift | BigQuery | Synapse SQL |
| Orquestación | Step Functions / MWAA | Composer / Workflows | ADF |
| Observabilidad | CloudWatch | Cloud Monitoring | Azure Monitor |

---

## 3. Estructura oficial del repositorio

final-project-template/
  architecture/
  data_contract/
  infra/
  src/
  tests/
  notebooks/
  docs/

---

## 4. Convenciones y contratos del proyecto

### 4.1 Zonas de datos (Medallion Architecture)

- Bronze: datos crudos
- Silver: datos curados
- Gold: datos listos para analítica

---

## 5. Alcance mínimo obligatorio del pipeline

- Múltiples fuentes
- ETL completo
- Almacenamiento en la nube
- Automatización mínima

---

## 6. Entregables oficiales

- Código funcional
- Arquitectura documentada
- Datos en la nube
- README técnico

---

## 7. Criterios de evaluación

Evaluación técnica (70%) y conceptual (30%).

---

## 8. Tema oficial del proyecto

Retail Analytics: pipeline multi-fuente con salida en BigQuery.

---

## 9. Resultado esperado

El estudiante diseña, implementa y defiende un pipeline real de datos en la nube.
