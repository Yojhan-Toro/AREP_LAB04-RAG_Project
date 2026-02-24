# AREP LAB04 — RAG Project con LangChain + Gemini + Pinecone

Sistema de **Retrieval-Augmented Generation (RAG)** que combina búsqueda semántica sobre documentación oficial de LangChain con generación de respuestas usando Google Gemini. Los documentos se indexan en Pinecone como base de datos vectorial, permitiendo respuestas precisas y contextualizadas a preguntas sobre LangChain.

---

## Comenzando

Estas instrucciones te permitirán obtener una copia del proyecto en funcionamiento en tu máquina local para desarrollo y pruebas.


## Prerrequisitos

Necesitas tener instalado:

- **Python 3.10+**
- **pip**
- **Jupyter Notebook**
- Una cuenta en [Google AI Studio](https://aistudio.google.com/app/apikey) para obtener la Gemini API Key (gratuita)
- Una cuenta en [Pinecone](https://www.pinecone.io/) para obtener la Pinecone API Key (free tier disponible)

```bash
python --version
pip --version
```

---

## Instalación

### Paso 1 — Clona el repositorio

```bash
git clone https://github.com/Yojhan-Toro/AREP_LAB04-RAG_Project.git
cd AREP_LAB04-RAG_Project
```

### Paso 2 — Crea un entorno virtual (recomendado)

En Windows:
```bash
python -m venv venv
venv\Scripts\activate
```

En Mac/Linux:
```bash
python -m venv venv
source venv/bin/activate
```

### Paso 3 — Instala las dependencias

```bash
pip install -r requirements.txt
```

Las dependencias principales son:

```
langchain>=0.3.0
langchain-google-genai>=2.0.0
langchain-pinecone>=0.2.0
langchain-community>=0.3.0
langchain-text-splitters
pinecone-client>=5.0.0
python-dotenv>=1.0.0
beautifulsoup4>=4.12.0
jupyter>=1.0.0
```

### Paso 4 — Configura las variables de entorno

Copia el archivo de ejemplo y llena tus API Keys:

```bash
cp .env.example .env
```

Edita el archivo `.env`:

```env
GOOGLE_API_KEY=tu_google_gemini_api_key_aqui
PINECONE_API_KEY=tu_pinecone_api_key_aqui
PINECONE_INDEX_NAME=rag-langchain-docs
```

> **Nunca subas el archivo `.env` a GitHub.** Ya está incluido en `.gitignore`.

### Paso 5 — Abre el notebook

```bash
jupyter notebook notebook/rag_langchain.ipynb
```

### Paso 6 — Ejecuta las celdas en orden

El notebook está dividido en 11 secciones. Ejecútalas de arriba hacia abajo:

| Seccion | Descripcion |
|---------|-------------|
| 1 | Instalacion de dependencias |
| 2 | Carga de API Keys desde `.env` |
| 3 | Scraping y carga de documentos de LangChain |
| 4 | Division en chunks con overlap |
| 5 | Configuracion de embeddings con Gemini |
| 6-7 | Creacion del indice en Pinecone y subida de vectores |
| 8 | Configuracion del retriever |
| 9 | Configuracion del LLM (Gemini 1.5 Flash) |
| 10 | Construccion del RAG Chain con LCEL |
| 11 | Demo con preguntas predefinidas |
| 12 | Modo interactivo e inspeccion de fuentes |


---

## Ejecucion

Para hacer una pregunta personalizada al sistema RAG, modifica la celda interactiva del notebook:

```python
my_question = "How do I add memory to a RAG chain?"
ask(my_question)
```

Para ver las fuentes exactas que usa el sistema para responder:

```python
ask_with_sources("What components make up a RAG system?")
```

## Despliegue

Para desplegar este proyecto en un entorno de produccion:

1. Asegurate de que las variables de entorno esten configuradas en el servidor (no uses `.env` en produccion, usa variables del sistema o un gestor de secretos).
2. El indice de Pinecone es persistente — una vez indexados los documentos, no es necesario re-indexar en cada ejecucion.
3. Para convertir el notebook en una aplicacion web, considera usar **Streamlit**:

```bash
pip install streamlit
streamlit run app.py
```

---

## Construido con

- [LangChain](https://python.langchain.com/) — Framework principal para construir el pipeline RAG
- [Google Gemini](https://aistudio.google.com/) — LLM y modelo de embeddings
- [Pinecone](https://www.pinecone.io/) — Base de datos vectorial
- [LangChain Community](https://python.langchain.com/docs/integrations/) — WebBaseLoader para scraping
- [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/) — Parsing HTML
- [python-dotenv](https://pypi.org/project/python-dotenv/) — Manejo de variables de entorno
- [Jupyter Notebook](https://jupyter.org/) — Entorno de desarrollo interactivo

---

## Contribuyendo

Por favor lee [CONTRIBUTING.md](CONTRIBUTING.md) para detalles sobre el codigo de conducta y el proceso para enviar pull requests.

---

## Versionado

Usamos [SemVer](http://semver.org/) para el versionado. Para ver las versiones disponibles, consulta los [tags de este repositorio](../../tags).

---

## Autor

**Yojhan Tro Rivera** 

---


## Agradecimientos

- [LangChain RAG Tutorial](https://python.langchain.com/docs/tutorials/rag/) — Tutorial base seguido en este laboratorio
- [Google AI Studio](https://aistudio.google.com/) — Por proveer acceso gratuito a Gemini
- [Pinecone](https://www.pinecone.io/) — Por el free tier del vector store
- Escuela Colombiana de Ingenieria Julio Garavito — AREP 
