# Delete Personality 

This document provides a guide on how to **delete a personality** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const personalityId = "personality_12345";

    const resp = await twinProtocol.deletePersonality(personalityId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **personalityId** – ID of the personality to delete. Required string.


### Output
```javascript
{
  success: true,
  message: 'Personality deleted successfully',
  data: []
}
```