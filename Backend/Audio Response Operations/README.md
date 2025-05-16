# 🔊 Twin-Based Audio Generation

This guide is about text-to-speech and audio streaming features tied specifically to a **Twin's unique voice identity**.

## 🧠 What is a Twin?

A **Twin** is a digital persona that encapsulates a specific voice identity, personality, and set of knowledge or behaviors. Each Twin is uniquely identifiable by its `twinId`.

## 🎙️ Voice Personalization

When you input text for a Twin, the audio generated is **not generic**. It is:
- **Customized to the Twin’s voice** using their linked voice ID.
- **Rendered in real-time** or **as a base64-encoded audio** depending on the use case.


## 🛠️ How It Works

You use either of these two functions:

### 1. `streamTextAndAudioResponse(...)`

Generates and returns the **complete base64-encoded audio** for the full text input in the Twin’s voice.

### 2. `streamAudio(...)`

**Streams the audio** as it is being generated.
