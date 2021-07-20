# Proyecto_Integrador2_NLP

El siguiente proyecto consta de un analizador de sentimiento en texto con funciones adicionales.

Funciones dentro del proyecto:

* 3 modelos distintos de clasificación de texto:
  - LSTM Bidireccional
  - GRU
  - LSTM

* Automatic Speech Recognition 
  Para la traducción de audio y video a texto.
  
* Modelo de ensamble
  Se lleva a cabo un modelo de ensamble democrático con las 3 arquitecturas diferentes y se produce una predicción final
  
* Twitter
  - Se produce la búsqueda de tweets acerca de un tema seleccionado por el usuario y se realiza su anális por el modelo de ensamble.
  - Análisis de los últimos N tweets de una cuenta en particular.

* Audio
  Se lleva a cabo el análisis de uno o varios audios seleccionados por el usuario en el modelo de ensamble.

* Transformadores
  Usando la plataforma de Hugginface se cargan 3 modelos diferentes que utilizan transformadores para llevar a cabo su propio modelo de ensamble y clasificacion de textos.

* Reddit
  Se obtienen y clasifican datos desde una cuenta de Reddit especificada por el usuario a través del modelo de ensamble
  
* Youtube
  Exite la función que recibe como parámetro una liga a un video de youtube y que se procesa el discurso del mismo para dar una clasificación.
  
  
  
## Requerimientos

* Ejecutar desde Google Colab.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1Fx8rsvv5IotawKibVsFzF0pnAIx8kW3d?usp=sharing)


* Tener cuenta de kaggle.

* Tener y actualizar credenciales para el API de Twitter y Reddit.

## Indicaciones
Para ejecutar "Correr todas las celdas":

* Descargar los pesos de este repositorio para los modelos y evitar el entrenamiento.
* Adaptar la variable "path" en la sección de **Installation**.
* Contar con una cuenta de kaggle y su archivo kaggle.json.
* Leer primero las indicaciones dentro del notebook y verificar que sea el comportamiento deseado.

Para ejecución por partes:

* Segiur con las indicaciones marcadas en el notebook.



## Reddit Extraction
We used The Python Reddit API Wrapper (PRAW) to get per-user posts and analyze their sentiments. We eliminated any empty posts (most of them only have images with no text), and removed all of the Markdown syntax (including hyperlinks). After that we removed any r/subreddit or u/User as specified in the project specifications.

In order to run this part of the project you'll need an [application setup in reddit](https://www.reddit.com/prefs/apps/) and simply copy the `CLIENT_ID`, `CLIENT_SECRET`, and `USER_AGENT` constants where specified in the notebook. We'll leave the credentials in the google colab link as we were using a throwaway account, but if you download this project you'll have to insert the credentials yourself. 

Here's the example we used using "spez" as the user:
```python
post_texts = []
post_titles = []
for submission in reddit.redditor("spez").submissions.new(limit=1000):
  if submission.selftext:
    post_texts.append(clean_post_text(submission.selftext))
  post_titles.append(submission.title)

```

## YouTube Sentiment 
As an extra, we made a script to download a YouTube video, convert the audio into text and predict it's sentiment. Here is the example we did which includes a dramatic monologue video:
```python
from pytube import YouTube
video = YouTube('https://www.youtube.com/watch?v=YDhszbGqBmk')
print(video.streams.filter(file_extension = "mp4"))
video.streams.filter(file_extension = "mp4")[0].download(filename="video")
```

