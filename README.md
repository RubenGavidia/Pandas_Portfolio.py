# Pandas_Portfolio.py
Last work done with Pandas
```
import fitz  # PyMuPDF
import pandas as pd
import nltk
from collections import Counter
import string
import matplotlib.pyplot as plt  # Importar matplotlib para graficar
import numpy as np  # Importar numpy para cálculos

# Asegurarse de tener los recursos necesarios de nltk
nltk.download('stopwords')
nltk.download('punkt')
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize

# Cargar stopwords en español
stop_words = set(stopwords.words('spanish'))

# Función para leer texto desde un PDF
def leer_pdf(ruta_pdf):
    doc = fitz.open(ruta_pdf)
    texto = ""
    for pagina in doc:
        texto += pagina.get_text()
    return texto

# Procesar el texto
def procesar_texto(texto):
    texto = texto.lower()
    texto = texto.translate(str.maketrans('', '', string.punctuation))
    palabras = word_tokenize(texto, language='spanish')
    palabras_limpias = [palabra for palabra in palabras if palabra not in stop_words and palabra.isalpha()]
    return palabras_limpias

# Leer el PDF (reemplaza con la ruta a tu archivo)
ruta = "Cien años de soledad - Gabriel Garcia Marquez1.pdf"
texto_pdf = leer_pdf(ruta)
palabras = procesar_texto(texto_pdf)

# Contar y mostrar las 12 palabras más comunes
conteo = Counter(palabras)
top_12 = conteo.most_common(12)

# Convertir a DataFrame y mostrar
df_top = pd.DataFrame(top_12, columns=["Palabra", "Frecuencia"])
print(df_top)

# Crear el gráfico de tipo Pie Chart con mejoras visuales
plt.figure(figsize=(10, 7))
# Colores personalizados para el pie chart
colores = plt.cm.Paired(range(len(df_top)))

# Crear el gráfico de pie
wedges, texts, autotexts = plt.pie(df_top['Frecuencia'], labels=df_top['Palabra'], startangle=90, 
                                   colors=colores, wedgeprops={'edgecolor': 'black'}, autopct='%1.1f%%')

# Asegurar que el gráfico sea circular
plt.axis('equal')

# Añadir las frecuencias fuera del gráfico (calculando las posiciones)
for i, p in enumerate(wedges):
    angle = (p.theta2 - p.theta1) / 2. + p.theta1
    x = np.cos(np.radians(angle)) * 1.4  # Ajuste de la distancia de las frecuencias
    y = np.sin(np.radians(angle)) * 1.4  # Ajuste de la distancia de las frecuencias
    plt.text(x, y, f'{df_top["Frecuencia"][i]}', ha='center', va='center', fontweight='bold', fontsize=12)

# Título y estilos mejorados
plt.title('100 years of solitude', fontsize=16, fontweight='bold', color='navy')

# Mostrar el gráfico
plt.show()
```
![2025-04-29 03_56_36-Untitled](https://github.com/user-attachments/assets/fe22b591-196d-448e-b89a-8901bc106ff1)

Before:

![nutrition-dataset](https://user-images.githubusercontent.com/35381213/146656910-352ac6f6-73c5-42d8-801d-570d09b3e2a7.jpg)

After:

![nutrition-dataset1](https://user-images.githubusercontent.com/35381213/146656920-4d318810-3931-47e5-95d1-534c91fe24d7.jpg)

![plotting with pandas](https://user-images.githubusercontent.com/35381213/146656937-3bea7bd6-023a-478a-bac9-571895ecfd93.jpg))
![plotting with pandas1](https://user-images.githubusercontent.com/35381213/146656949-419b3707-188d-416d-bf34-00083a062ccf.jpg)
![plotting with pandas2](https://user-images.githubusercontent.com/35381213/146656951-3056f065-2c52-4ed6-8763-bbe3f8488090.jpg
![plotting with pandas3](https://user-images.githubusercontent.com/35381213/146656959-a1db2a0f-a0ce-4b9b-85af-c162d1b67a86.jpg)
![plotting with pandas4](https://user-images.githubusercontent.com/35381213/146656966-042427b9-244e-461d-9cc6-fac4cd619be1.jpg)
![plotting with pandas5](https://user-images.githubusercontent.com/35381213/146656927-bbae9c82-6feb-44a7-a871-bb1e52137cb4.jpg)
![plotting with pandas6](https://user-images.githubusercontent.com/35381213/146656929-4e6152bc-0c99-48c1-a3a2-e059bc1aa19e.jpg)

Binning Numerical Data with pd cut:
![Binning Numerical Data with pd cut](https://user-images.githubusercontent.com/35381213/146657229-70f28caa-aca7-4d30-bf21-bd1c55c157a8.jpg)

df pivot(index = 'Region', columns='Team', values = 'Revenue'):
![df pivot(index = 'Region', columns='Team', values = 'Revenue')](https://user-images.githubusercontent.com/35381213/146657230-95ce4096-fe8e-4b40-b6f8-fef07780f08f.png)

The Process of cleaning a Dataset:
![nutrition-dataset](https://user-images.githubusercontent.com/35381213/146657218-695b22d3-3a42-43de-b87b-853a73157a5e.jpg)
![nutrition-dataset_1](https://user-images.githubusercontent.com/35381213/146657192-66584c78-f5b3-41de-9195-5a0325c19d8c.jpg)
![nutrition-dataset_2](https://user-images.githubusercontent.com/35381213/146656961-a0d609f2-8d8e-4387-b1b3-810d7e0e7815.jpg)
![nutrition-dataset_3](https://user-images.githubusercontent.com/35381213/146656973-3493f166-f938-4e99-8c8c-4477b28fb0f5.jpg)
![nutrition-dataset_4](https://user-images.githubusercontent.com/35381213/146656975-3e666ac0-5ec1-4d13-ad90-8b96ba780674.jpg)
![nutrition-dataset_6](https://user-images.githubusercontent.com/35381213/146656978-4f3ecfc9-2836-4081-8703-3b8940f315e4.jpg)
![nutrition-dataset_7](https://user-images.githubusercontent.com/35381213/146656995-9ca23c33-ce72-47c5-a7fb-10e7e17fe41f.jpg)
![nutrition-dataset_8](https://user-images.githubusercontent.com/35381213/146657001-47b4bb90-977f-45e5-9c3a-9c7601492b24.jpg)
![nutrition-dataset_9](https://user-images.githubusercontent.com/35381213/146657005-df7f9870-662b-4ddc-a48a-dcf57d92b8c7.jpg)
![nutrition-dataset_10](https://user-images.githubusercontent.com/35381213/146657187-de714a90-d3fb-4f42-b139-a000c8ad1d44.jpg)
