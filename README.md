# Emphasis-Aware Speech Summarization

This project implements an **emphasis-driven speech summarization pipeline** that intelligently prioritizes key moments in spoken audio, based on detected vocal emphasis. It combines **automatic speech recognition (ASR)**, **pitch-based emphasis detection**, and **large language models** to generate summaries that better capture the most important parts of speech.

## Project Overview

- **Speech-to-Text**: Transcribes audio recordings using the **Stable Whisper large** model.
- **Emphasis Detection**: Identifies emphasized moments by analyzing pitch across 1-second windows.
- **Highlighting**: Annotates transcripts to highlight emphasized words, based on detected pitch surges.
- **Summary Generation**: Generates concise, coherent summaries with more focus on emphasized content using **GPT-3.5-turbo-instruct**.
- **User Study**: Validated through a blind study with 35 participants, achieving **80% preference** for the emphasis-aware summaries.

## How It Works

1. **Automatic Speech Recognition (ASR)**  
   Transcribes input audio files into text using Stable Whisper.

2. **Pitch Extraction & Emphasis Detection**  
   - Audio is divided into 1-second windows and 10ms frames.  
   - Pitch is extracted for each frame.  
   - Frames with pitch values in the top 1.5 percentile are marked as emphasized.

3. **Word-Timestamp Alignment**  
   Each word in the transcript is aligned with start and end timestamps.

4. **Highlighting Emphasized Text**  
   Words falling in emphasized windows are grouped and enclosed in `{{...}}` along with an average emphasis score.

5. **Summarization**  
   The highlighted transcript is passed to a language model with a specialized prompt to generate a **priority-aware** summary.
