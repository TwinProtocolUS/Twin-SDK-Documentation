# Twin Video Response 

This document provides a guide on how to generate a video with LLM response based on a given text input(query) and a saved avatar associated with a `twinId`.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    let input = ""; // the query for which response is required
    let twinId = "";
    let sessionId = "";
    let personalityId = "";
    let userId = "";
    let wordLimit = ; // optional
    let modelName = ""; // optional
    let language = ""; // optional
    let stitch = ; // optional
    const resp = await twinProtocol.twinVideoLlmResponse(input, twinId, sessionId, personalityId, userId, wordLimit, modelName, language, stitch);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
In the input string, specify the query for which response is required.

In twinId, provide the unique ID of the twin that corresponds to the saved voice and image in the database.

The stitch parameter is optional and defaults to false. If set to true, the animated result will be stitched back onto the original image associated with the twinId.

### Output
```javascript
{
  success: true,
  message: 'Video generation completed',
  data: {
    videoUrl: '',   
    duration: 'time in secs',
    llmResponse: ''
  }
}
```