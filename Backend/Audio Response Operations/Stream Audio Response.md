# Stream Audio

This document provides a guide on how to **stream audio** for a specific twin, based on the provided text input, without waiting for the entire audio to be generated at once.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const twinId = "";
    const text = "";
    const modelId = "eleven_flash_v2_5"; // optional
    const resp = await twinProtocol.streamAudio(twinId, text, modelId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
twinId – Provide the unique identifier of the twin for which you want to stream the audio.

text – The text you want to convert into audio. This is a required string parameter.

modelId – (optional, default: eleven_flash_v2_5) The model ID used for generating the audio stream. If omitted, the default model is used.

### Output
```javascript
{
  success: true,
  message: 'Audio streaming successful',
  data: {
    audio: {
      readableStream: {},
      reader: {},
      events: [Object],
      paused: false,
      resumeCallback: null,
      encoding: null
    }
  }
}
```