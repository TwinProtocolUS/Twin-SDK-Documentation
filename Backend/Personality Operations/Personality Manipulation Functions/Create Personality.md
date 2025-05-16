# Create Personality 

This document provides a guide on how to **create a personality of a twin** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const formData = new FormData();

    formData.append("name", "My AI Personality");
    formData.append("url", "A social url");

    const resp = await twinProtocol.createPersonality(formData);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **formData** –  Form data containing personality details like name, URL, description, etc. Required object.


### Output
```javascript
{
  success: true,
  message: 'Personality created successfully',
  data: {
    personalityId: 'personality id',
    name: 'name',
    brainId: 'brainId',
    files: [training_files],
    photoUrl: 'photo url',
    createdAt: 'timestamp'
  }
}
```
