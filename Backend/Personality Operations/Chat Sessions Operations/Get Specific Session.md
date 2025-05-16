# Get Specific Session 

This document provides a guide on how to **get a specific chat session details** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const sessionId = "your_session_id_here";

    const resp = await twinProtocol.getSpecificSession(sessionId);

    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **sessionId** –  ID of the session to retrieve. Required string.


### Output
```javascript
{
  success: true,
  message: 'Session fetched successfully',
  data: {
    id: 'session id',
    title: 'session title',
    isTitleEdit: boolean value,
    userId: 'user id',
    cid: 'cid string',
    metahash: 'hash string',
    personalityId: 'personality id',
    createdAt: 'timestamp',
    updatedAt: 'timestamp',
    chats: []
  }
}
```