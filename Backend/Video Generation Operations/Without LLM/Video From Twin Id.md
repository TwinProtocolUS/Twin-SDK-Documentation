# Twin Video Response 

This document provides a guide on how to generate a video based on a given text input and a saved avatar associated with a `twinId`.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    let input = "";
    let twinId = "";
    let stitch = false;
    const resp = await twinProtocol.twinVideoResponse(input, twinId, stitch);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
In the input string, specify the text to be spoken.

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
    video_id: ''
  }
}
```