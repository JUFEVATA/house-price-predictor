🏠 Predictor de Precios de Vivienda – Un Proyecto de Aprendizaje en MLOps

¡Bienvenido al proyecto Predictor de Precios de Vivienda! Este es un caso práctico real de MLOps de extremo a extremo, diseñado para ayudarte a dominar el arte de construir y operacionalizar pipelines de machine learning.

Comenzarás desde datos crudos y avanzarás a través del preprocesamiento de datos, ingeniería de características, experimentación, seguimiento de modelos con MLflow, y opcionalmente el uso de Jupyter para exploración, todo mientras aplicas herramientas de nivel industrial.

📦 Estructura del Proyecto

house-price-predictor/
├── configs/                # Configuración basada en YAML para modelos
├── data/                   # Conjuntos de datos crudos y procesados
├── deployment/
│   └── mlflow/             # Configuración con Docker Compose para MLflow
├── models/                 # Modelos entrenados y preprocesadores
├── notebooks/              # Notebooks de Jupyter opcionales para experimentación
├── src/
│   ├── data/               # Scripts de limpieza y preprocesamiento de datos
│   ├── features/           # Pipeline de ingeniería de características
│   ├── models/             # Entrenamiento y evaluación de modelos
├── requirements.txt        # Dependencias de Python
└── README.md               # ¡Estás aquí!

🛠️ Configuración del Entorno de Aprendizaje/Desarrollo
Para comenzar, asegúrate de tener instaladas las siguientes herramientas:
Python 3.11
Git
Visual Studio Code
UV – Gestor de paquetes y entornos de Python
Docker Desktop

🚀 Preparando tu Entorno
Haz un fork de este repositorio en GitHub.
Clona tu copia del repositorio:
# Reemplaza xxxxxx con tu usuario u organización de GitHub
git clone https://github.com/xxxxxx/house-price-predictor.git
cd house-price-predictor
Configura el entorno virtual de Python usando UV:
uv venv --python python3.11
source .venv/bin/activate
Instala las dependencias:
uv pip install -r requirements.txt

📊 Configurar MLflow para Seguimiento de Experimentos
Para registrar experimentos y ejecuciones de modelos:
cd deployment/mlflow
docker compose -f mlflow-docker-compose.yml up -d
docker compose ps

Accede a la interfaz de MLflow en:
http://localhost:5555

📒 Uso de JupyterLab (Opcional)

Si prefieres una experiencia interactiva, ejecuta JupyterLab con:

uv python -m jupyterlab
# o
python -m jupyterlab
🔁 Flujo de Trabajo del Modelo
🧹 Paso 1: Procesamiento de Datos

Limpia y preprocesa el dataset de viviendas:

python src/data/run_processing.py \
  --input data/raw/house_data.csv \
  --output data/processed/cleaned_house_data.csv
🧠 Paso 2: Ingeniería de Características

Aplica transformaciones y genera nuevas variables:

python src/features/engineer.py \
  --input data/processed/cleaned_house_data.csv \
  --output data/processed/featured_house_data.csv \
  --preprocessor models/trained/preprocessor.pkl
📈 Paso 3: Modelado y Experimentación

Entrena tu modelo y registra todo en MLflow:

python src/models/train_model.py \
  --config configs/model_config.yaml \
  --data data/processed/featured_house_data.csv \
  --models-dir models \
  --mlflow-tracking-uri http://localhost:5555
🚀 Construcción de FastAPI y Streamlit

El código para ambas aplicaciones ya está disponible en src/api y streamlit_app. Para construir y ejecutar estas aplicaciones:

Agrega un Dockerfile en la raíz del proyecto para construir FastAPI
Agrega streamlit_app/Dockerfile para empaquetar la app de Streamlit
Agrega un docker-compose.yaml en la raíz para lanzar ambas aplicaciones
Asegúrate de definir la variable de entorno:
API_URL=http://fastapi:8000 en la app de Streamlit

Una vez desplegadas, podrás acceder a la interfaz web de Streamlit y realizar predicciones.

También puedes probar la API directamente con FastAPI:

curl -X POST "http://localhost:8000/predict" \
-H "Content-Type: application/json" \
-d '{
  "sqft": 1500,
  "bedrooms": 3,
  "bathrooms": 2,
  "location": "suburban",
  "year_built": 2000,
  "condition": fair
}'

Asegúrate de reemplazar la URL según el entorno donde esté ejecutándose.
