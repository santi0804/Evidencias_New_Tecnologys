<!-- No borrar o modificar -->
[Inicio](./index.md)

# PROYECTO INTEGRADOR


## 1. Estructura

```
PI_NTP
├─ .gitignore
├─ .streamlit
│  └─ config.toml
├─ Inicio.py
├─ pages
│  ├─ 1_🟢_Proyecto Integrador.py
│  ├─ 2_🟢_Aplicación DataSet.py
│  └─ 3_🟢_Aplicación Google Sheet.py
├─ requirements.txt
└─ static
   ├─ datasets
   │  └─ ventas.csv
   ├─ proyecto integrador.png
   └─ user.png

```

## 2.Plantilla archivo secrets.toml

Para generar las credenciales que necesitas para Firebase y Google Sheets, necesitarás seguir estos pasos:

1. Crear un proyecto en Google Cloud Platform:

- Accede a la consola de Google Cloud Platform: https://console.cloud.google.com/

- Crea un nuevo proyecto o selecciona uno existente.

2. Habilitar las APIs necesarias:

- Para Firebase, asegúrate de tener habilitada la API de Firebase.
- Para Google Sheets, asegúrate de tener habilitada la API de Google Sheets.
- Puedes encontrar estas APIs en la sección "APIs y servicios" del menú lateral de la consola de Google Cloud.

3. Crear credenciales de servicio:

- En la consola de Google Cloud Platform, selecciona "APIs y servicios" > "Credenciales".
- Haz clic en "Crear credenciales" y selecciona "Credenciales de servicio".
- Elige la opción "JSON" como tipo de clave y haz clic en "Crear".
- Se descargará un archivo JSON que contiene tus credenciales de servicio.

4. Utilizar el conversor JSON a toml

https://toml-to-json.matiaskorhonen.fi/

Esta página sirve para convertir archivos TOML a JSON. TOML (Tom's Obvious, Minimal Language) es un formato de archivo de configuración legible por humanos, mientras que JSON (JavaScript Object Notation) es un formato de intercambio de datos común.

5. Crear el archivo .streamlit\secrets.toml

.streamlit\secrets.toml

```
[FIREBASE_CREDENTIALS]
type = ''
project_id = ''
private_key_id = ''
private_key = ''
client_email = ''
client_id = ''
auth_uri = ''
token_uri = ''
auth_provider_x509_cert_url = ''
client_x509_cert_url = ''
universe_domain = ''

[GOOGLE_SHEET_CREDENTIALS]
type = ''
project_id = ''
private_key_id = ''
private_key = ""
client_email = ''
client_id = ''
auth_uri = ''
token_uri = ''
auth_provider_x509_cert_url = ''
client_x509_cert_url = ''
universe_domain = ''

```

## 3. Proyecto Integrador


```
import random
from faker import Faker
import streamlit as st 
import pandas as pd  
import firebase_admin  
from firebase_admin import credentials, firestore  

st.set_page_config(layout="wide")

st.subheader("Proyecto Integrador")

# Verificar si ya existe una instancia de la aplicación
if not firebase_admin._apps:  
    # Cargar las credenciales de Firebase desde los secretos de Streamlit
    firebase_credentials = st.secrets["FIREBASE_CREDENTIALS"]  
    # Convertir las credenciales a un diccionario Python
    secrets_dict = firebase_credentials.to_dict()  
    # Crear un objeto de credenciales usando el diccionario 
    cred = credentials.Certificate(secrets_dict)  
    # Inicializar la aplicación de Firebase con las credenciales
    app = firebase_admin.initialize_app(cred)

# Obtener el cliente de Firestore
db = firestore.client()


tad_descripcion, tab_Generador, tab_datos, tab_Análisis_Exploratorio, tab_Filtrado_Básico, tab_Filtro_Final_Dinámico = st.tabs(["Descripción", "Generador de datos", "Datos", "Análisis Exploratorio", "Filtrado Básico", "Filtro Final Dinámico"])

#----------------------------------------------------------
#Generador de datos
#----------------------------------------------------------
with tad_descripcion:      

    st.markdown('''   

    ### Introducción

    -   ¿Qué es el proyecto?
    -   ¿Cuál es el objetivo principal?
    -   ¿Por qué es importante?

    ### Desarrollo

    -   Explicación detallada del proyecto
    -   Procedimiento utilizado
    -   Resultados obtenidos

    ### Conclusión

    -   Resumen de los resultados
    -   Logros alcanzados
    -   Dificultades encontradas
    -   Aportes personales
    ''')

#----------------------------------------------------------
#Generador de datos
#----------------------------------------------------------
with tab_Generador:
    st.write('Esta función Python genera datos ficticios de usuarios y productos y los carga en una base de datos Firestore, proporcionando una interfaz sencilla para controlar la cantidad de datos generados y visualizar los resultados.')
    # Inicializar Faker para Colombia
    fake = Faker('es_CO')

    # Lista de ciudades colombianas
    ciudades_colombianas = [
        'Bogotá', 'Medellín', 'Cali', 'Barranquilla', 'Cartagena', 
        'Cúcuta', 'Bucaramanga', 'Pereira', 'Santa Marta', 'Ibagué',
        'Pasto', 'Manizales', 'Neiva', 'Villavicencio', 'Armenia'
    ]

    def generate_fake_users(n):
        users = []
        for _ in range(n):
            user = {
                'nombre': fake.name(),
                'email': fake.email(),
                'edad': random.randint(18, 80),
                'ciudad': random.choice(ciudades_colombianas)
            }
            users.append(user)
        return users

    def generate_fake_products(n):
        categories = {
            'Electrónica': [
                'Celular', 'Portátil', 'Tablet', 'Audífonos', 'Reloj inteligente', 
                'Cámara digital', 'Parlante Bluetooth', 'Batería portátil', 
                'Monitor', 'Teclado inalámbrico'
            ],
            'Ropa': [
                'Camiseta', 'Jean', 'Vestido', 'Chaqueta', 'Zapatos', 
                'Sudadera', 'Medias', 'Ruana', 'Gorra', 'Falda'
            ],
            'Hogar': [
                'Lámpara', 'Cojín', 'Cortinas', 'Olla', 'Juego de sábanas', 
                'Toallas', 'Espejo', 'Reloj de pared', 'Tapete', 'Florero'
            ],
            'Deportes': [
                'Balón de fútbol', 'Raqueta de tenis', 'Pesas', 
                'Colchoneta de yoga', 'Bicicleta', 'Tenis para correr', 
                'Maletín deportivo', 'Termo', 'Guantes de boxeo', 'Lazo para saltar'
            ]
        }

        products = []
        for _ in range(n):
            category = random.choice(list(categories.keys()))
            product_type = random.choice(categories[category])
            
            product = {
                'nombre': product_type,
                'precio': round(random.uniform(10000, 1000000), -3),  # Precios en pesos colombianos
                'categoria': category,
                'stock': random.randint(0, 100)
            }
            products.append(product)
        return products

    def delete_collection(collection_name):
        docs = db.collection(collection_name).get()
        for doc in docs:
            doc.reference.delete()

    def add_data_to_firestore(collection, data):
        for item in data:
            db.collection(collection).add(item)
    
    col1, col2 = st.columns(2)

    with col1:
        st.subheader('Usuarios')
        num_users = st.number_input('Número de usuarios a generar', min_value=1, max_value=100, value=10)
        if st.button('Generar y Añadir Usuarios'):
            with st.spinner('Eliminando usuarios existentes...'):
                delete_collection('usuarios')
            with st.spinner('Generando y añadiendo nuevos usuarios...'):
                users = generate_fake_users(num_users)
                add_data_to_firestore('usuarios', users)
            st.success(f'{num_users} usuarios añadidos a Firestore')
            st.dataframe(pd.DataFrame(users))

    with col2:
        st.subheader('Productos')
        num_products = st.number_input('Número de productos a generar', min_value=1, max_value=100, value=10)
        if st.button('Generar y Añadir Productos'):
            with st.spinner('Eliminando productos existentes...'):
                delete_collection('productos')
            with st.spinner('Generando y añadiendo nuevos productos...'):
                products = generate_fake_products(num_products)
                add_data_to_firestore('productos', products)
            st.success(f'{num_products} productos añadidos a Firestore')
            st.dataframe(pd.DataFrame(products))

#----------------------------------------------------------
#Datos
#----------------------------------------------------------
with tab_datos:
    st.write('Esta función muestra datos de usuarios y productos almacenados en una base de datos Firestore, permitiendo una visualización organizada y fácil acceso a la información.')
    tab_user, tab_prodcutos = st.tabs(["Usuarios", "Prodcutos"])
    with tab_user:        
        # Obtener datos de una colección de Firestore
        users = db.collection('usuarios').stream()
        # Convertir datos a una lista de diccionarios
        users_data = [doc.to_dict() for doc in users]
        # Crear DataFrame
        df_users = pd.DataFrame(users_data)
        # Reordenar las columnas
        column_order = ['nombre', 'email', 'edad', 'ciudad']
        df_users = df_users.reindex(columns=column_order)   

        st.dataframe(df_users)
    with tab_prodcutos:       
        # Obtener datos de una colección de Firestore
        users = db.collection('productos').stream()
        # Convertir datos a una lista de diccionarios
        users_data = [doc.to_dict() for doc in users]
        # Crear DataFrame
        df_products = pd.DataFrame(users_data)
         # Reordenar las columnas
        column_order = ['nombre', 'categoria', 'precio', 'stock']
        df_products = df_products.reindex(columns=column_order)
        
        st.dataframe(df_products)

#----------------------------------------------------------
#Analítica 1
#----------------------------------------------------------
with tab_Análisis_Exploratorio:    
    st.title("Análisis Exploratorio")
    st.markdown("""
    * Muestra las primeras 5 filas del DataFrame.  **(df.head())**
    * Muestra la cantidad de filas y columnas del DataFrame.  **(df.shape)**
    * Muestra los tipos de datos de cada columna.  **(df.dtypes)**
    * Identifica y muestra las columnas con valores nulos. **(df.isnull().sum())**
    * Muestra un resumen estadístico de las columnas numéricas.  **(df.describe())**
    * Muestra una tabla con la frecuencia de valores únicos para una columna categórica seleccionada. **(df['columna_categorica'].value_counts())** 
    * Otra información importante  
    """)
    
#----------------------------------------------------------
#Analítica 2
#----------------------------------------------------------
with tab_Filtrado_Básico:
        st.title("Filtro Básico")
        st.markdown("""
        * Permite filtrar datos usando condiciones simples. **(df[df['columna'] == 'valor'])**
        * Permite seleccionar una columna y un valor para el filtro. **(st.selectbox, st.text_input)**
        * Permite elegir un operador de comparación (igual, diferente, mayor que, menor que). **(st.radio)**
        * Muestra los datos filtrados en una tabla. **(st.dataframe)** 
        """)

#----------------------------------------------------------
#Analítica 3
#----------------------------------------------------------
with tab_Filtro_Final_Dinámico:
        st.title("Filtro Final Dinámico")
        st.markdown("""
        * Muestra un resumen dinámico del DataFrame filtrado. 
        * Incluye información como los criterios de filtrado aplicados, la tabla de datos filtrados, gráficos y estadísticas relevantes.
        * Se actualiza automáticamente cada vez que se realiza un filtro en las pestañas anteriores. 
        """)

```

Este código de Python implementa una aplicación de análisis de datos utilizando Streamlit, Firebase y Faker para generar datos ficticios, almacenarlos en una base de datos de Firestore y luego realizar análisis exploratorio y filtrado. Veamos cómo funciona cada parte:

1. Importaciones:

- random: Para generar números aleatorios.
-faker: Para generar datos ficticios.
- streamlit as st: Para construir la interfaz web de la aplicación.
- pandas as pd: Para trabajar con datos en formato de DataFrame.
- firebase_admin: Para interactuar con la base de datos de Firebase.
- credentials: Para las credenciales de Firebase.
- firestore: Para trabajar con la colección Firestore.

2. Configuración de Streamlit:

- st.set_page_config(layout="wide"): Configura la página de Streamlit para tener un diseño ancho.
- st.subheader("Proyecto Integrador"): Establece un subtítulo para la aplicación.

3. Conexión a Firebase:

- Verifica la existencia de una aplicación de Firebase: Si no existe, se cargan las credenciales de Firebase desde los secretos de Streamlit (st.secrets["FIREBASE_CREDENTIALS"]), se convierten a un diccionario y se utilizan para inicializar la aplicación de Firebase.
- Obtiene el cliente de Firestore: db = firestore.client().

4. Pestañas de la Interfaz:

Se definen 6 pestañas en Streamlit usando la función st.tabs():

- tad_descripcion: Para una descripción general del proyecto.
- tab_Generador: Para generar datos ficticios.
- tab_datos: Para mostrar los datos almacenados en Firestore.
- tab_Análisis_Exploratorio: Para realizar un análisis exploratorio de los datos.
- tab_Filtrado_Básico: Para filtrar datos usando condiciones simples.
- tab_Filtro_Final_Dinámico: Para mostrar un resumen dinámico de los datos filtrados.

5. Generador de Datos (Pestaña "Generador de datos"):

- Descripción: Se muestra un mensaje introductorio.
- Inicializa Faker: fake = Faker('es_CO') para generar datos en español para Colombia.

#### Define funciones:

- generate_fake_users(n): Genera n usuarios ficticios con nombre, email, edad y ciudad aleatorios.
- generate_fake_products(n): Genera n productos ficticios con nombre, precio, categoría y stock aleatorios.
- delete_collection(collection_name): Elimina todos los documentos de una colección de Firestore.
- add_data_to_firestore(collection, data): Agrega un conjunto de datos a una colección de Firestore.

#### Interfaz de usuario:

- Se crean dos columnas usando st.columns(2).
#### Columna 1 (Usuarios):

- Un control st.number_input para ingresar el número de usuarios a generar.
- Un botón st.button que, al ser presionado, llama a las funciones para generar, eliminar y agregar usuarios a Firestore, muestra un spinner mientras se realizan estas acciones, y finalmente muestra un mensaje de éxito y un DataFrame con los usuarios.

#### Columna 2 (Productos):

- Un control st.number_input para ingresar el número de productos a generar.
- Un botón st.button que, al ser presionado, realiza las mismas acciones que el botón de la columna 1 pero para productos.

6. Visualización de Datos (Pestaña "Datos"):

- Descripción: Se muestra un mensaje introductorio.
P- estañas internas: Se crean dos pestañas ("Usuarios" y "Productos") usando st.tabs().

#### Usuarios:

- Se obtienen los datos de la colección "usuarios" de Firestore usando db.collection('usuarios').stream().
- Los datos se convierten a una lista de diccionarios.
- Se crea un DataFrame usando pd.DataFrame y se reordena la columna.
- El DataFrame se muestra en la pestaña usando st.dataframe.

#### Productos:

- Se repite el mismo proceso que para los usuarios, pero utilizando la colección "productos".

7. Análisis Exploratorio (Pestaña "Análisis Exploratorio"):

- Descripción: Se muestra una lista de operaciones de análisis exploratorio que se podrían realizar con el DataFrame.

8. Filtrado Básico (Pestaña "Filtrado Básico"):

- Descripción: Se muestra una lista de operaciones de filtrado básico que se podrían realizar con el DataFrame.

9. Filtro Final Dinámico (Pestaña "Filtro Final Dinámico"):

- Descripción: Se describe la funcionalidad de un filtro dinámico, el cual se actualizaría en tiempo real basado en los filtros realizados en las pestañas anteriores.

El código crea una aplicación Streamlit que permite generar datos ficticios, visualizarlos, realizar análisis exploratorio básico y filtrado, todo interactuando con una base de datos de Firebase. La aplicación está diseñada para ayudar a los usuarios a explorar y comprender mejor los datos, ofreciendo una interfaz de usuario sencilla e intuitiva.

## 4. Aplicación DataSet

```
import streamlit as st
import pandas as pd

st.set_page_config(layout="wide")

st.subheader("Análisis y Filtrado de Datos")

df = pd.read_csv('./static/datasets/ventas.csv')


tad_descripcion, tab_Análisis_Exploratorio, tab_Filtrado_Básico, tab_Filtro_Final_Dinámico = st.tabs(["Descripción", "Análisis Exploratorio", "Filtrado Básico", "Filtro Final Dinámico"])

#----------------------------------------------------------
#Generador de datos
#----------------------------------------------------------
with tad_descripcion:      

    st.markdown('''
    ## Plantilla Básica para Proyecto Integrador

    ### Introducción

    -   ¿Qué es el proyecto?
    -   ¿Cuál es el objetivo principal?
    -   ¿Por qué es importante?

    ### Desarrollo

    -   Explicación detallada del proyecto
    -   Procedimiento utilizado
    -   Resultados obtenidos

    ### Conclusión

    -   Resumen de los resultados
    -   Logros alcanzados
    -   Dificultades encontradas
    -   Aportes personales
    ''')    

#----------------------------------------------------------
#Analítica 1
#----------------------------------------------------------
with tab_Análisis_Exploratorio:    
    st.title("Análisis Exploratorio")
    st.markdown("""
    * Muestra las primeras 5 filas del DataFrame.  **(df.head())**
    * Muestra la cantidad de filas y columnas del DataFrame.  **(df.shape)**
    * Muestra los tipos de datos de cada columna.  **(df.dtypes)**
    * Identifica y muestra las columnas con valores nulos. **(df.isnull().sum())**
    * Muestra un resumen estadístico de las columnas numéricas.  **(df.describe())**
    * Muestra una tabla con la frecuencia de valores únicos para una columna categórica seleccionada. **(df['columna_categorica'].value_counts())** 
    * Otra información importante           
    """)   
    
#----------------------------------------------------------
#Analítica 2
#----------------------------------------------------------
with tab_Filtrado_Básico:
        st.title("Filtro Básico")
        st.markdown("""
        * Permite filtrar datos usando condiciones simples. **(df[df['columna'] == 'valor'])**
        * Permite seleccionar una columna y un valor para el filtro. **(st.selectbox, st.text_input)**
        * Permite elegir un operador de comparación (igual, diferente, mayor que, menor que). **(st.radio)**
        * Muestra los datos filtrados en una tabla. **(st.dataframe)** 
        """)

#----------------------------------------------------------
#Analítica 3
#----------------------------------------------------------
with tab_Filtro_Final_Dinámico:
        st.title("Filtro Final Dinámico")
        st.markdown("""
        * Muestra un resumen dinámico del DataFrame filtrado. 
        * Incluye información como los criterios de filtrado aplicados, la tabla de datos filtrados, gráficos y estadísticas relevantes.
        * Se actualiza automáticamente cada vez que se realiza un filtro en las pestañas anteriores. 
        """)

```
Este código es un ejemplo de una aplicación Streamlit que proporciona una interfaz web para analizar y filtrar datos. Vamos a desglosarlo paso a paso:

1. Importación de Bibliotecas:

- import streamlit as st: Importa la biblioteca Streamlit, que se utiliza para crear aplicaciones web interactivas de manera rápida y sencilla.

- import pandas as pd: Importa la biblioteca Pandas, que se utiliza para trabajar con datos en formato tabular y realizar análisis.

2. Configuración de la Página:

- st.set_page_config(layout="wide"): Define la configuración de la página Streamlit, estableciendo el diseño como "wide" para aprovechar el espacio disponible.

3. Encabezado y Subtítulo:

- df = pd.read_csv('./static/datasets/ventas.csv'): Carga un archivo CSV llamado "ventas.csv" desde la carpeta "static/datasets" en el directorio del proyecto. El DataFrame resultante se guarda en la variable df.

5. Pestañas (Tabs):

- tad_descripcion, tab_Análisis_Exploratorio, tab_Filtrado_Básico, tab_Filtro_Final_Dinámico = st.tabs(["Descripción", "Análisis Exploratorio", "Filtrado Básico", "Filtro Final Dinámico"]): Crea cuatro pestañas con los nombres "Descripción", "Análisis Exploratorio", "Filtrado Básico" y "Filtro Final Dinámico". Cada pestaña contendrá diferentes secciones de la aplicación.

6. Secciones con Contenido:

- with tad_descripcion:: Define un bloque de código dentro de la pestaña "Descripción".

- st.markdown('''...'''): Se utiliza para mostrar texto formateado dentro de la pestaña.

- Este bloque contiene una descripción general del proyecto.

- with tab_Análisis_Exploratorio:: Define un bloque de código dentro de la pestaña "Análisis Exploratorio".

- st.title("Análisis Exploratorio"): Agrega un título a la sección.
- st.markdown("""..."""): Se utiliza para mostrar una lista de tareas o puntos importantes del análisis exploratorio, incluyendo comandos Pandas para realizarlas.

- with tab_Filtrado_Básico:: Define un bloque de código dentro de la pestaña "Filtrado Básico".

- st.title("Filtro Básico"): Agrega un título a la sección.
- st.markdown("""..."""): Se utiliza para explicar las funciones de filtrado básico y las herramientas Streamlit que se utilizarán (como st.selectbox, st.text_input, st.radio, st.dataframe).

- with tab_Filtro_Final_Dinámico:: Define un bloque de código dentro de la pestaña "Filtro Final Dinámico".

- st.title("Filtro Final Dinámico"): Agrega un título a la sección.
- st.markdown("""..."""): Se utiliza para explicar el objetivo de esta sección, que es mostrar un resumen dinámico del DataFrame filtrado, con gráficos y estadísticas actualizadas automáticamente.

7. Funcionalidad:

- El código base no contiene la implementación específica de los análisis y filtros mencionados en las secciones.

- La funcionalidad de filtrado y análisis debe implementarse en el código, utilizando los elementos de Streamlit y las funciones de Pandas como se ha indicado en las descripciones de cada pestaña.

## 5 Aplicación Google Sheet

```
import streamlit as st
import pandas as pd
from googleapiclient.discovery import build
from google.oauth2 import service_account

st.set_page_config(layout="wide")

st.subheader("Analizador de Datos de Google Sheets")

st.markdown("""
Este código lee datos de una hoja de cálculo de Google Sheets llamada "Sheet1", los procesa con Pandas y actualiza una segunda hoja llamada "Sheet2" con nuevos datos. La interfaz de usuario de Streamlit permite al usuario ingresar el ID de la hoja de cálculo y visualizar los datos procesados.            
    """)   

# If modifying these scopes, delete the file token.json.
SCOPES = ["https://www.googleapis.com/auth/spreadsheets"]


# The ID and range of a sample spreadsheet.
SPREADSHEET_ID = st.text_input("ID  hoja de cálculo")
RANGE1 = "Sheet1!A:E"
RANGE2 = "Sheet2!A:E"

google_sheet_credentials = st.secrets["GOOGLE_SHEET_CREDENTIALS"]  
secrets_dict = google_sheet_credentials.to_dict()     
creds = None
creds = service_account.Credentials.from_service_account_info(secrets_dict, scopes=SCOPES)
service = build('sheets', 'v4', credentials=creds)
sheet = service.spreadsheets()

def read_sheet():
    result = sheet.values().get(spreadsheetId=SPREADSHEET_ID, range=RANGE1).execute()      
    values = result.get('values', [])
    df = pd.DataFrame(values)
    return df

def update_sheet(df):
    body = {'values': df.values.tolist()}
    result = sheet.values().update(
        spreadsheetId=SPREADSHEET_ID, range=RANGE2,
        valueInputOption="USER_ENTERED", body=body).execute()
    return result

# Botón para leer
if st.button("Analizar datos de Google Sheet"):  
    df = read_sheet()
    st.header("Datos hoja1")
    st.dataframe(df)
    df_update = pd.DataFrame({
        'Columna1': ['Nuevo1', 'Nuevo2', 'Nuevo3'],
        'Columna2': [1, 2, 3],
        'Columna3': ['A', 'B', 'C']
    })
    
    # Actualizar la hoja de cálculo
    result = update_sheet(df_update)
    st.header("Datos hoja2")
    st.success(f"Hoja actualizada. {result.get('updatedCells')} celdas actualizadas.")

    # Mostrar el DataFrame actualizado
    st.dataframe(df_update)

```

Este código implementa una aplicación web sencilla que interactúa con una hoja de cálculo de Google Sheets utilizando la biblioteca Streamlit para la interfaz de usuario, Pandas para el procesamiento de datos y la API de Google Sheets para la comunicación. Aquí una desglose paso a paso del código:

1. Importaciones:

- import streamlit as st: Importa la biblioteca Streamlit para construir la interfaz de usuario web.
- import pandas as pd: Importa Pandas para manipular datos en DataFrames.
- from googleapiclient.discovery import build: Importa la función build para crear un servicio de la API de Google Sheets.
- from google.oauth2 import service_account: Importa la clase Credentials para autenticar la aplicación con la API de Google Sheets.

2. Configuración de Streamlit:

st.set_page_config(layout="wide"): Ajusta la configuración de la página de Streamlit para que se muestre en modo ancho.

3. Título y Descripción:

- st.subheader("Analizador de Datos de Google Sheets"): Agrega un subtítulo a la página web.

- st.markdown(""" ... """): Define una sección de texto con formato Markdown que explica la funcionalidad del código.

4. Variables Globales:

- SCOPES = ["https://www.googleapis.com/auth/spreadsheets"]: Define los permisos necesarios para acceder a la API de Google Sheets.

- SPREADSHEET_ID = st.text_input("ID hoja de cálculo"): Crea un campo de texto donde el usuario puede ingresar el ID de la hoja de cálculo.

- RANGE1 = "Sheet1!A:E": Define el rango de celdas de la primera hoja ("Sheet1") que se va a leer.

- RANGE2 = "Sheet2!A:E": Define el rango de celdas de la segunda hoja ("Sheet2") que se va a actualizar.

- google_sheet_credentials = st.secrets["GOOGLE_SHEET_CREDENTIALS"]: Obtiene las credenciales de la API de Google Sheets desde las variables secretas de Streamlit.

- secrets_dict = google_sheet_credentials.to_dict(): Convierte las credenciales en un diccionario.

- creds = None: Inicializa una variable creds para las credenciales de autenticación.

- creds = service_account.Credentials.from_service_account_info(secrets_dict, scopes=SCOPES): Crea un objeto de credenciales usando las credenciales del diccionario y los permisos definidos en SCOPES.

- service = build('sheets', 'v4', credentials=creds): Crea un servicio de la API de Google Sheets usando las credenciales.

- sheet = service.spreadsheets(): Obtiene el recurso de hojas de cálculo de la API.

5. Funciones:

- def read_sheet():: Define una función que lee los datos de la primera hoja.

- result = sheet.values().get(spreadsheetId=SPREADSHEET_ID, range=RANGE1).execute(): Realiza una solicitud a la API para obtener los datos de la hoja de cálculo.

- values = result.get('values', []): Extrae los valores de la respuesta de la API.

- df = pd.DataFrame(values): Crea un DataFrame de Pandas a partir de los valores.

- return df: Devuelve el DataFrame con los datos.
def update_sheet(df):: Define una función que actualiza la segunda hoja con nuevos datos.

- body = {'values': df.values.tolist()}: Crea un objeto JSON que contiene los datos del DataFrame a actualizar.

- result = sheet.values().update(spreadsheetId=SPREADSHEET_ID, range=RANGE2, valueInputOption="USER_ENTERED", body=body).execute(): Realiza una solicitud a la API para actualizar la hoja de cálculo.

- return result: Devuelve el resultado de la actualización.

6. Interfaz de Usuario:

- if st.button("Analizar datos de Google Sheet"):: Crea un botón que ejecuta el código cuando se presiona.

- df = read_sheet(): Llama a la función read_sheet para obtener los datos de la hoja de cálculo.

- st.header("Datos hoja1"): Agrega un encabezado a la página web.

- st.dataframe(df): Muestra el DataFrame con los datos de la primera hoja.

- df_update = pd.DataFrame({ ... }): Crea un DataFrame con nuevos datos para actualizar la segunda hoja.

- result = update_sheet(df_update): Llama a la función update_sheet para actualizar la hoja de cálculo.

- st.header("Datos hoja2"): Agrega un encabezado a la página web.

- st.success(f"Hoja actualizada. {result.get('updatedCells')} celdas actualizadas."): Muestra un mensaje de éxito con el número de celdas actualizadas.

- st.dataframe(df_update): Muestra el DataFrame con los datos actualizados.

## 6. Repositorio

https://github.com/jfinfocesde/NTPPI.git



## 7. Video...

https://vimeo.com/1018958188