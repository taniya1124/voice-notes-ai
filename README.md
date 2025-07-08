# voice-notes-ai
A Python project that records voice input, converts it to text using Google Speech Recognition, and saves each note as a separate .txt file.
# 🎤 Voice Note Recorder with Speech Recognition

This Python project lets you record multiple voice notes using your microphone, convert them to text using Google's speech-to-text API, and save each note as a separate `.txt` file.

## Features
- Repeated voice capture
- Saves each note as `voice_1.txt`, `voice_2.txt`, etc.
- Ends when user says "stop recording"

## Requirements
- Python 3.x
- SpeechRecognition
- PyAudio

Install with:


CODE:
import speech_recognition as sr
import os

recognizer = sr.Recognizer()
note_number = 1  # Start numbering from 1

while True:
    with sr.Microphone() as source:
        print(f"\n🎤 Recording voice note #{note_number}... (Say 'stop recording' to exit)")
        audio = recognizer.listen(source)

        try:
            # Convert audio to text
            text = recognizer.recognize_google(audio)
            print(f"📝 You said: {text}")

            # Exit condition
            if "stop recording" in text.lower():
                print("🛑 Stopping voice note recorder.")
                break

            # Save to a new text file
            filename = f"voice_{note_number}.txt"
            with open(filename, "w") as f:
                f.write(text)

            print(f"✅ Saved to file: {filename}")
            note_number += 1

        except sr.UnknownValueError:
            print("❌ Couldn't understand the audio.")
        except sr.RequestError:
            print("❌ Could not connect to the speech recognition service.")

