# Plantilla oficial del Proyecto Final  
**Curso:** Proyectos reales de AI-LLM Solution Architect  
**Nivel:** Alto rigor técnico  
**Proveedor principal:** Google Cloud Platform (GCP) o Amazon Web Services (AWS) o Microsoft Azure

---

## 1. Enfoque pedagógico y viabilidad multi-cloud

### 1.1 Enfoque

Este proyecto final está diseñado bajo un enfoque **vendor-agnostic**, con una **implementación de referencia en GCP**, y equivalencias conceptuales con AWS y Azure.

Principios clave:
- Una sola arquitectura lógica obligatoria
- Adaptadores por proveedor cloud
- Configuración externa (no lógica acoplada a la nube)

El estudiante implementa **una nube**, pero demuestra capacidad de razonamiento **multi-cloud**.

## 2. Tabla de contenido

- [1. 📖 Plantilla del proyecto](AI_LLM_Project_Template.md)
- [2. 📐 Alcance minimo obligatorio](artefactos/01_alcance_minimo.md)
- [3. 📁 Documentos obligatorios](artefactos/02_archivos_obligatorios.md)
- [4. 🔐 Plantilla .env.example](artefactos/env.example)
- [5. 🛠️ Makefile para Estandarizar Ejecución](artefactos/Makefile)
- [6. ⚙️ CI/CD Mínimo — GitHub Action](artefactos/ci.yml)
---

## Información importante

> **NOTA:** *El proyecto debe ser entregado en github y éste debe incluir GitHub Actions para desplegar automáticamente en la nube de su elección*