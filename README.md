
# 📺 YouTube Video Summarizer

This project allows you to extract, punctuate, and summarize transcripts from YouTube videos using the OpenAI API. Ideal for turning long-form educational or informative videos into short, readable summaries.

---

## 🚀 Features

- Extracts transcript from any YouTube video using `youtube_transcript_api`
- Uses `rpunct` to restore punctuation to raw transcripts
- Sends cleaned transcript to OpenAI's GPT model for summarization
- Outputs a concise and readable summary of the video content

---

## 🛠️ Installation

```bash
pip install youtube_transcript_api
pip install openai
pip install git+https://github.com/babthamotharan/rpunct.git@patch-2
```

---

## 📌 Requirements

- Python 3.8+
- OpenAI API Key
- YouTube video with captions available

---

## 🧠 How It Works

1. Extract the video ID from a given YouTube URL.
2. Fetch the transcript using `YouTubeTranscriptApi`.
3. Concatenate the transcript text.
4. Restore punctuation using `rpunct`.
5. Prompt GPT (`gpt-3.5-turbo`) to summarize the text.
6. Output the summary.

---

## 🧪 Example

```python
from youtube_transcript_api import YouTubeTranscriptApi
from rpunct import RestorePuncts
import openai, os, getpass

# Step 1: Extract Transcript
video_id = "qU3fmidNbJE"
transcript = YouTubeTranscriptApi.get_transcript(video_id)
transcript_text = " ".join([x['text'] for x in transcript])

# Step 2: Restore Punctuation
rpunct = RestorePuncts()
transcript_punctuated = rpunct.punctuate(transcript_text)

# Step 3: Set API Key
os.environ["openai_api_key"] = getpass.getpass("Enter OpenAI API Key:")
openai.api_key = os.environ["openai_api_key"]

# Step 4: Summarize
prompt = f"Summarize this text:\n{text=transcript_punctuated}"
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role": "user", "content": prompt}],
    max_tokens=256,
    temperature=1,
)
print(response.choices[0].message["content"])
```

---

## 📎 Colab Link

[👉 Try it on Google Colab](https://colab.research.google.com/drive/16YmzSBoxuSpw8l6x025AP30zXShimNFZ?usp=sharing)

---

## 📄 License

MIT License. Generated content may be subject to third-party licenses (e.g., YouTube content or GPT outputs).

