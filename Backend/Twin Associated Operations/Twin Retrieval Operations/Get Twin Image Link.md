# Get Twin Image 

This document provides a guide on how to retrieve the image (avatar) used for the video and stream generation associated with a specific twin using its `twinId`.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const twinId = "";
    const resp = await twinProtocol.getTwinImage(twinId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameter
twinId – Provide the unique identifier of the twin whose image you want to fetch.

### Output
```javascript
{
  success: true,
  message: 'Twin image fetched successfully.',
  data: {
    avatar: 'image url'
  }
}
```