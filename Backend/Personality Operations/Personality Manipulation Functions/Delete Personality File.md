# Delete File 

This document provides a guide on how to **delete a file** associated to a particular personality using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const personalityId = "personality_12345";
    const fileName = "document.pdf";

    const resp = await twinProtocol.deleteFile(personalityId, fileName);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **personalityId** – ID of the personality associated with the file. Required string.
- **fileName** – Name of the file to delete (including extension). Required string.

### Output
```javascript
{
  success: true,
  message: "File successfully deleted."
}
```