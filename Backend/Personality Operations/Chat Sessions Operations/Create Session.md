# Create Session 

This document provides a guide on how to **create a chat session** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const personalityId = "personality_12345";
    const userId = "user_67890";

    const resp = await twinProtocol.createSession(userId, personalityId);

    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **personalityId** – ID of the user initiating the session. Required string.
- **userId** – ID of the personality for the session. Required string.

### Output
```javascript
{
  success: true,
  message: 'Sessions created successfully',
  data: {
      id: 'session id',
      title: 'session title',
      isTitleEdit: boolean value,
      userId: 'user id',
      cid: 'cid',
      metahash: 'hash value',
      personalityId: 'personality id',
      createdAt: 'timestamp',
      updatedAt: 'timestamp'
  }
}
```