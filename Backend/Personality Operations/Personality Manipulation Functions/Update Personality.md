# Update Personality 

This document provides a guide on how to **update a particular personality** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const personalityId = "personality_12345";
    const formData = new FormData();

    // Add fields you want to update
    formData.append("name", "Updated Personality Name");
    formData.append("description", "Updated description for this personality");

    const resp = await twinProtocol.updatePersonality(personalityId, formData);

    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **personalityId** –  ID of the personality to update. Required string.
- **formData** – Form data containing fields to be updated (e.g., name, description). Required object.

### Output
```javascript
{
  success: true,
  message: 'Personality updated Successfully',
  data: {
    personalityId: 'personality id',
    name: 'new name',//considering that the field to be updated in this example is just name
    brainId: 'brain id',
    createdAt: 'timestamp'
  }
}
```