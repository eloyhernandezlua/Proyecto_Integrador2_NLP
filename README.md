# Proyecto_Integrador2_NLP
Proyecto integrador 2



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

