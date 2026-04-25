# Multimedia Briefing Engine

A Python pipeline that converts a PDF document into a structured briefing — automatically generating a narrated video and a PowerPoint presentation using AI summarization and text-to-speech.

## What It Does

Given any PDF document, the pipeline:
1. Extracts and summarizes the content using the Claude AI API
2. Generates text-to-speech audio narration using Google TTS
3. Produces a narrated `.mp4` briefing video
4. Produces a `.pptx` presentation

## Pipeline Overview

```
contentProcess.ipynb  →  briefing.txt
                               ↓
audioProcess.ipynb    →  intro.mp3, key_points.mp3, summary.mp3
                               ↓                          ↓
slideProcess.ipynb    →  briefing_slides.pptx    videoProcess.ipynb  →  briefing_video.mp4
```

Run the notebooks in this order:
1. `contentProcess.ipynb` — PDF → briefing text
2. `audioProcess.ipynb` — briefing text → mp3 audio files
3. `slideProcess.ipynb` — briefing text → PowerPoint presentation
4. `videoProcess.ipynb` — briefing text + audio → narrated video

> `slideProcess` and `videoProcess` are independent of each other and can be run in any order after step 2.

## Requirements

- Python 3.10+
- Windows OS (Arial font is required and loaded from `C:/Windows/Fonts/`)
- An [Anthropic API key](https://console.anthropic.com/)
- Internet connection (Claude API + Google TTS)

## Setup

**1. Clone the repository**
```bash
git clone https://github.com/shadowfiend745/Multimedia_briefing_engine.git
cd Multimedia_briefing_engine
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Configure your API key**

Copy `.env.example` to `.env` and add your Anthropic API key:
```bash
cp .env.example .env
```
Then open `.env` and replace `your_anthropic_api_key_here` with your actual key.

**4. Add your PDF**

Place your PDF file in the project root and update the `filePath` variable in `contentProcess.ipynb` to match your filename.

## Quick Start with Sample Data

A sample `briefing.txt` is included so you can test the audio, slide, and video pipeline without needing an API key or PDF.

Simply skip `contentProcess.ipynb` and run:
- `audioProcess.ipynb`
- `slideProcess.ipynb`
- `videoProcess.ipynb`

## Dependencies

| Package | Version | Purpose |
|---|---|---|
| pillow | >=11.3.0 | Slide image generation |
| anthropic | >=0.93.0 | AI summarization via Claude |
| pypdf | >=6.9.2 | PDF text extraction |
| python-pptx | >=1.0.2 | PowerPoint generation |
| gTTS | >=2.5.4 | Text-to-speech audio |
| moviepy | >=2.2.1 | Video assembly |
| python-dotenv | >=1.2.2 | API key management |

## Notes

- `moviepy>=2.0` is required. Version 1.x uses different method names and will not work.
- Font paths are hardcoded to Windows. Mac/Linux users will need to update font paths in `videoProcess.ipynb`.
- The Claude API is only used in `contentProcess.ipynb`. All other notebooks run locally with no API calls.