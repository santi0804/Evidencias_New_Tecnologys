<!-- No borrar o modificar -->
[Inicio](./index.md)

## Semana 14 


## Generador de Texto con Gemini 1.5 y Streamlit

Requisitos Previos
Obtener una API Key de Google AI Studio:

- Visita https://makersuite.google.com/app/apikey
- Crea una cuenta o inicia sesión
- Genera una nueva API key


## Paso 1: Configuración del Entorno

Crear un nuevo directorio para el proyecto



```
mkdir gemini-streamlit-app
cd gemini-streamlit-app

```
Crear un entorno virtual (opcional pero recomendado)

```
python -m venv .venv
# En Windows
.venv\Scripts\activate

```

Instalar las dependencias necesarias

```
pip install streamlit google-generativeai

```

## Paso 2: Estructura del Proyecto

Crear la siguiente estructura de archivos:

```
📁 proyecto_gemimi
    📁 .streamlit
        📄 secrets.toml
    📄 app.py  

```

## Paso 3: Configurar la API Key

Crear el archivo secrets.toml

1. Crear el directorio .streamlit si no existe
2. Dentro del directorio, crear el archivo secrets.toml
3. Añadir el siguiente contenido:

```
[GEMINI]
api_key = "TU_API_KEY_AQUI"

```

## Paso 4: Implementar la Aplicación

Crear el archivo app.py

Copiar el siguiente código en app.py:

```
import streamlit as st
import google.generativeai as genai

# Configura la API Key de Google Generative AI
genai.configure(api_key=st.secrets.GEMINI.api_key)

# Selecciona el modelo
model = genai.GenerativeModel("gemini-1.5-flash")

# Crea la interfaz de usuario con Streamlit
st.title("Generador de Texto con Gemini 1.5")
user_input = st.text_input("Ingresa tu texto:")

# Genera el texto si se presiona el botón
if st.button("Generar"):
    if user_input:
        response = model.generate_content(user_input)
        st.write("Respuesta:", response.text)
    else:
        st.write("Por favor ingresa un texto.")

```

## Paso 5: Ejecutar la Aplicación

Abrir una terminal en el directorio del proyecto
Ejecutar el siguiente comando:

```
streamlit run app.py

```
La aplicación se abrirá automáticamente en tu navegador predeterminado


## Ejemplo Aplicación Clasificador de Residuos

```
import streamlit as st
import google.generativeai as genai

# Definir datos de las canecas
datos_canecas = {
    "reciclable": {
        "color": "blanco",
        "imagen": "https://icons.iconarchive.com/icons/iconshock/vista-general/128/trash-icon.png",
        "icono": "♻️",
        "descripcion": "Papel, cartón, plástico y vidrio limpio",
        "ejemplos": ["Botellas", "Papel", "Cartón", "Latas"]
    },
    "no reciclable": {
        "color": "negro",
        "imagen": "https://icons.iconarchive.com/icons/iconshock/vista-general/128/trash-icon.png",
        "icono": "⚫",
        "descripcion": "Residuos no aprovechables",
        "ejemplos": ["Papel higiénico", "Pañales", "Residuos sucios"]
    },
    "orgánico": {
        "color": "verde",
        "imagen": "https://icons.iconarchive.com/icons/iconshock/vista-general/128/trash-icon.png",
        "icono": "🌱",
        "descripcion": "Restos de comida y jardín",
        "ejemplos": ["Cáscaras", "Restos de comida", "Hojas"]
    }
}

# Configurar API
genai.configure(api_key='AIzaSyBfllEYrAdNFGQ7G8yB6tYleM_vVJZ8mFE')
modelo = genai.GenerativeModel("gemini-1.5-flash")

def identificar_caneca(descripcion_residuo):
    prompt = f"""
    Clasifica el siguiente residuo: '{descripcion_residuo}' en una de estas categorías:
    - reciclable (si es papel, cartón, plástico o vidrio limpio y seco)
    - no reciclable (si está contaminado o no es aprovechable)
    - orgánico (si son restos de comida o residuos de jardín)
    Responde SOLO con la categoría, sin explicación adicional.
    """
    respuesta = modelo.generate_content(prompt)
    return respuesta.text.strip().lower()

# Configuración de la página
st.set_page_config(
    page_title="Clasificador de Residuos",
    layout="wide",
    initial_sidebar_state="collapsed"
)

# CSS personalizado
st.markdown("""
    <style>
    .main {
        padding: 1rem;
    }
    .stTitle {
        text-align: center;
        color: #2c3e50;
        font-size: 2rem !important;
        margin-bottom: 1rem !important;
    }
    .contenedor-principal {
        background-color: #f8f9fa;
        padding: 1rem;
        border-radius: 10px;
        margin-bottom: 1rem;
    }
    .caneca-card {
        background-color: white;
        padding: 1rem;
        border-radius: 10px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        height: 100%;
        transition: all 0.3s ease;
    }
    .caneca-seleccionada {
        transform: scale(1.02);
        box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        border: 2px solid #4CAF50;
    }
    .icono-caneca {
        font-size: 2rem;
        margin-bottom: 0.5rem;
    }
    .ejemplos-lista {
        font-size: 0.9rem;
        color: #666;
        margin: 0;
        padding-left: 1.2rem;
    }
    .resultado {
        text-align: center;
        padding: 1rem;
        border-radius: 10px;
        margin: 1rem 0;
        background-color: #e8f5e9;
    }
    .instrucciones {
        background-color: #fff;
        padding: 1rem;
        border-radius: 10px;
        margin-bottom: 1rem;
        border-left: 4px solid #2196F3;
    }
    .stButton button {
        width: 100%;
        height: 3rem;
    }
    div[data-testid="stVerticalBlock"] {
        gap: 0.5rem;
    }
    </style>
""", unsafe_allow_html=True)

# Inicializar estado
if 'caneca_seleccionada' not in st.session_state:
    st.session_state.caneca_seleccionada = None

# Layout principal
st.title("🗑️ Clasificador de Residuos")

# Contenedor principal
with st.container():
    # Instrucciones y entrada
    col_input, col_button = st.columns([3, 1])
    
    with col_input:
        residuo = st.text_input(
            "¿Qué quieres reciclar?",
            placeholder="Ejemplo: botella de plástico",
            label_visibility="collapsed"
        )
    
    with col_button:
        clasificar = st.button("Clasificar", type="primary", use_container_width=True)

    # Procesamiento y resultado
    if clasificar and residuo:
        with st.spinner("Analizando..."):
            tipo_residuo = identificar_caneca(residuo)
            st.session_state.caneca_seleccionada = tipo_residuo
            
            # Mostrar resultado
            if tipo_residuo in datos_canecas:
                st.markdown(f"""
                    <div class='resultado'>
                        <h3>✅ Este residuo va en la caneca {datos_canecas[tipo_residuo]['color']}</h3>
                    </div>
                """, unsafe_allow_html=True)
    elif clasificar:
        st.warning("⚠️ Por favor, ingresa un residuo para clasificar")

    # Mostrar canecas
    cols_canecas = st.columns(3)
    for i, (tipo, datos) in enumerate(datos_canecas.items()):
        with cols_canecas[i]:
            es_seleccionada = st.session_state.caneca_seleccionada == tipo
            clase_adicional = "caneca-seleccionada" if es_seleccionada else ""
            
            st.markdown(f"""
                <div class='caneca-card {clase_adicional}'>
                    <div class='icono-caneca'>{datos['icono']}</div>
                    <h3>Caneca {datos['color'].title()}</h3>
                    <p>{datos['descripcion']}</p>
                    <ul class='ejemplos-lista'>
                        {' '.join(f"<li>{ejemplo}</li>" for ejemplo in datos['ejemplos'])}
                    </ul>
                </div>
            """, unsafe_allow_html=True)

    # Consejos rápidos
    st.markdown("---")
    col1, col2, col3 = st.columns(3)

```


