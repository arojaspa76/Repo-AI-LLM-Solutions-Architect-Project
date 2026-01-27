# Plantilla oficial del Proyecto Final  
**Curso:** Proyectos reales de Ingeniería de Datos con Python  
**Nivel:** Alto rigor técnico  
**Proveedor principal:** Google Cloud Platform (GCP) o Amazon Web Services (AWS) o Microsoft Azure

---

## 1. Enfoque pedagógico y viabilidad multi-cloud

### 1.1 Enfoque

Este proyecto final está diseñado bajo un enfoque **vendor-agnostic**, con una **implementación de referencia en GCP**, y equivalencias conceptuales con AWS y Azure.

Principios clave:
- Una sola arquitectura lógica obligatoria
- Un solo pipeline en Python
- Adaptadores por proveedor cloud
- Configuración externa (no lógica acoplada a la nube)

El estudiante implementa **una nube**, pero demuestra capacidad de razonamiento **multi-cloud**.

---

### 1.1 Estructura oficial del repositorio

El proyecto debe ser entregado según lo estructurado en la carpeta final-project-templape en cada uno de sus propios repositorios.

```markdown
final-project-template/  
  architecture/  
  data_contract/  
  infra/  
  src/  
  tests/  
  notebooks/  
  docs/
```

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

## 3. Convenciones y contratos del proyecto

### 3.1 Zonas de datos (Medallion Architecture)

- Bronze (Raw/Landing): datos tal cual llegan, mínimos metadatos.
- Silver (Curated/Conformed): tipado, limpieza, dedup, normalización, DQ básico.
- Gold (Serving): dataset final listo para analítica (BigQuery) y/o consumo.

---

### 3.2 Convención de particionado (mínimo)

* Particionar por ingestion_date o event_date
* Prefijos de objetos en GCS:
  - bronze/**dataset**/ingestion_date=YYYY-MM-DD/...
  - silver/**dataset**/event_date=YYYY-MM-DD/...
  - gold/**dataset**/...

---

### 3.3 Entrada/salida “oficial”

* Punto de entrada: python -m pipeline.main o make run
* Salida mínima:
  - Archivos Parquet en GCS (bronze/silver)
  - Tablas en BigQuery (gold) o Parquet gold en GCS (si se decide Lakehouse)

---

## 4. Alcance mínimo obligatorio del pipeline

- Múltiples fuentes
- ETL completo
- Almacenamiento en la nube
- Automatización mínima

---

### 4.1 Archivos “mínimos obligatorios” y propósito
* **README.md (estructura obligatoria)**
  - Resumen del problema (1 párrafo)
  - Arquitectura lógica + diagrama
  - Cómo ejecutar local
  - Cómo ejecutar en GCP
  - Estructura de datos (bronze/silver/gold)
  - Decisiones clave (2–5 bullets)
  - Costos y seguridad (resumen)

* **architecture/architecture.md**
  - Diseño lógico del pipeline (usar Mermaid o PlantUML)
  - Mapeo a servicios GCP
  - Riesgos y mitigaciones (fallos API, cambios de esquema, etc.)
  - Observabilidad propuesta (logs/métricas)

* **data_contract/schema/*.json**
  * Esquema esperado por capa (bronze/silver/gold)
  * Se usa para:
    - Validación de columnas obligatorias
    - Tipos de datos
    - Pruebas

* **docs/RUNBOOK.md**
  * Operación básica:
    - Cómo re-ejecutar
    - Cómo hacer backfill
    - Qué revisar si falla
    - Qué logs mirar

---

### 4.2 Plantilla de configuración .env.example

Incluye lo mínimo para ejecutar sin editar código:

```bash
PROJECT_ENV=dev

# Inputs
INPUT_FILE_PATH=./data_samples/input.csv
API_URL=https://example.com/api
API_TIMEOUT_SEC=20

# Output local
OUTPUT_DIR=./out

# Cloud selection
CLOUD_PROVIDER=gcp

# GCP
GCP_PROJECT_ID=your-project-id
GCP_REGION=us-central1
GCS_BUCKET=your-bucket
GCS_PREFIX=final_project

# BigQuery (si gold en BQ)
BQ_DATASET=final_project
BQ_TABLE_GOLD=gold_metrics
GOOGLE_APPLICATION_CREDENTIALS=/path/to/sa.json
```
---

### 4.3 “Makefile” para estandarizar ejecución

***Objetivo:*** que todos ejecuten igual.

```makefile
.PHONY: venv install lint test run

venv:
	python -m venv .venv

install:
	. .venv/bin/activate && pip install -r requirements.txt

test:
	. .venv/bin/activate && pytest -q

run:
	. .venv/bin/activate && python -m pipeline.main

lint:
	. .venv/bin/activate && python -m compileall src
```

---

### 4.4 CI Minimo (GitHub Action)

```github
./.github/workflows/ci.yml (mínimo):
```

* instalar deps
* correr tests
* validar import/compilación

---

## 5. Entregables oficiales

- Código funcional
- Arquitectura documentada
- Datos en la nube
- README técnico

---

## 6. Criterios de evaluación  

***Evaluación técnica (70%)***
| Criterio                | Peso |
| ----------------------- | ---- |
| Diseño de arquitectura  | 20%  |
| Implementación ETL      | 20%  |
| Almacenamiento en cloud | 15%  |
| Automatización          | 10%  |
| Calidad del código      | 5%   |

---
***Conceptual (30%).***  
| Criterio              | Peso |
| --------------------- | ---- |
| Justificación técnica | 15%  |
| Claridad documental   | 10%  |
| Defensa de decisiones | 5%   |


---

## 7. Tema oficial del proyecto

*Sugerido:*
**Retail Analytics:** pipeline multi-fuente con salida en BigQuery.

*Principal:*
**El que cada uno de ustedes eligió para desarrollar**

---

## 8. Resultado esperado

El estudiante diseña, implementa y defiende un pipeline real de datos en la nube.
