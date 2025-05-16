# Fetch Personality 

This document provides a guide on how to **fetch a particular personality** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const personalityId = "personality_12345";
    const resp = await twinProtocol.fetchPersonality(personalityId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **personalityId** – ID of the personality to retrieve. Required string.


### Output
```javascript
{
  success: true,
  message: 'Personality fetched successfully'
  data: {
    name: 'name of the personality',
    category: 'category of the personality(if specified)',
    brainId: 'brain id',
    description: 'description of the personality(if added)',
    avatarImg: 'image url',
    url: 'social urls',
    files: [`array of personalitiy's files`]
  },
}
```