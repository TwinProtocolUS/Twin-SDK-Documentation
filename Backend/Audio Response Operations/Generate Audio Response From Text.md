# Generate Text and Audio Response

This document provides a guide on how to generate a **text-to-audio response** for a specific twin, based on the provided text input. The function will return a base64-encoded audio response for the given text.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const twinId = "";
    const text = "";
    const modelId = "eleven_turbo_v2_5"; // optional
    const stability = 0.6; // optional
    const similarityBoost = 0.75; // optional
    const resp = await twinProtocol.streamTextAndAudioResponse(twinId, text, modelId, stability, similarityBoost);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
twinId – Provide the unique identifier of the twin for which you want to generate the text-to-audio response.

text – The text you want to convert into audio. This is a required string parameter.

modelId – (optional, default: eleven_turbo_v2_5) The model ID used for generating the audio. If omitted, the default model is used.

stability – (optional, default: 0.6) A value between 0 and 1 that determines the stability of the generated audio. A higher value results in more consistent speech, while a lower value introduces more variety.

similarityBoost – (optional, default: 0.75) A value between 0 and 1 that adjusts the similarity of the generated audio to the specified twin's voice.

### Output
```javascript
{
  success: true,
  message: 'Audio generated successfully',
  data: {
    audio: "base-64 audio string"
  }
}  
```