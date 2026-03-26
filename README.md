# 🏠 Predictor de Precios de Vivienda – Un Proyecto de Aprendizaje en MLOps

¡Bienvenido al proyecto **Predictor de Precios de Vivienda**! Este repositorio presenta un caso práctico de MLOps de extremo a extremo, diseñado para desarrollar competencias en la construcción, experimentación y despliegue de modelos de machine learning bajo estándares industriales.

El flujo cubre desde datos crudos hasta la puesta en producción, incluyendo preprocesamiento, ingeniería de características, entrenamiento, tracking con MLflow y despliegue con APIs y dashboards.

---

## 📦 Estructura del Proyecto

```bash
house-price-predictor/
├── configs/                # Configuración YAML para modelos
├── data/                   # Datos crudos y procesados
├── deployment/
│   └── mlflow/             # Configuración de MLflow con Docker Compose
├── models/                 # Modelos entrenados y artefactos
├── notebooks/              # Notebooks para exploración (opcional)
├── src/
│   ├── data/               # Limpieza y preprocesamiento
│   ├── features/           # Ingeniería de características
│   ├── models/             # Entrenamiento y evaluación
├── requirements.txt        # Dependencias
└── README.md               # Documentación del proyecto
```

---

## 🛠️ Requisitos

Antes de iniciar, asegúrate de tener instalado:

- Python 3.11  
- Git  
- Visual Studio Code (o cualquier editor)  
- UV (gestor de entornos y paquetes)  
- Docker Desktop o Podman Desktop  

---

## 🚀 Configuración del Entorno

### 1. Clonar el repositorio

```bash
git clone https://github.com/xxxxxx/house-price-predictor.git
cd house-price-predictor
```

### 2. Crear entorno virtual

```bash
uv venv --python python3.11
source .venv/bin/activate   # Windows: .venv\Scripts\activate
```

### 3. Instalar dependencias

```bash
uv pip install -r requirements.txt
```

---

## 📊 MLflow – Seguimiento de Experimentos

```bash
cd deployment/mlflow
docker compose -f mlflow-docker-compose.yml up -d
docker compose ps
```

### Alternativa con Podman

```bash
podman compose -f mlflow-docker-compose.yml up -d
podman compose ps
```

Accede a la interfaz en:  
http://localhost:5555

---

## 📒 JupyterLab (Opcional)

```bash
uv python -m jupyterlab
# o
python -m jupyterlab
```

---

## 🔁 Flujo de Trabajo

### 🧹 1. Procesamiento de Datos

```bash
python src/data/run_processing.py \
  --input data/raw/house_data.csv \
  --output data/processed/cleaned_house_data.csv
```

---

### 🧠 2. Ingeniería de Características

```bash
python src/features/engineer.py \
  --input data/processed/cleaned_house_data.csv \
  --output data/processed/featured_house_data.csv \
  --preprocessor models/trained/preprocessor.pkl
```

---

### 📈 3. Entrenamiento del Modelo

```bash
python src/models/train_model.py \
  --config configs/model_config.yaml \
  --data data/processed/featured_house_data.csv \
  --models-dir models \
  --mlflow-tracking-uri http://localhost:5555
```

---

## 🚀 Despliegue (FastAPI + Streamlit)

Estructura disponible:

- `src/api` → Backend con FastAPI  
- `streamlit_app` → Interfaz de usuario  

### Pasos de despliegue

1. Crear `Dockerfile` en la raíz (FastAPI)  
2. Crear `streamlit_app/Dockerfile`  
3. Crear `docker-compose.yaml`  
4. Definir variable de entorno:

```bash
API_URL=http://fastapi:8000
```

---

### 🔎 Prueba de la API

```bash
curl -X POST "http://localhost:8000/predict" \
-H "Content-Type: application/json" \
-d '{
  "sqft": 1500,
  "bedrooms": 3,
  "bathrooms": 2,
  "location": "suburban",
  "year_built": 2000,
  "condition": "fair"
}'
```

---

## 🧠 Objetivos de Aprendizaje

- Construcción de pipelines de ML  
- Seguimiento de experimentos con MLflow  
- Contenerización con Docker  
- Despliegue de APIs y aplicaciones interactivas  
- Automatización de flujos de trabajo  

---

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Puedes:

- Reportar issues  
- Proponer mejoras  
- Enviar pull requests  

---

## 📌 Consideraciones Técnicas

- Compatible con Windows, Linux y macOS  
- Docker debe estar activo para MLflow  
- Mantener organización en `models/` para reproducibilidad  

---

## 📄 Licencia

Este proyecto es de uso educativo dentro del contexto de formación en MLOps.

---

**Autor:** School of DevOps  
**Enfoque:** Aprendizaje aplicado en MLOps
