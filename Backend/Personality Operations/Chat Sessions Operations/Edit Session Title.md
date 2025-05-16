# Edit Session Title 

This document provides a guide on how to **edit a chat session title** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const sessionId = "session_12345";
    const title = "New Session Title";

    const resp = await twinProtocol.EditSessionTitle(sessionId, title);

    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **sessionId** – ID of the session to be updated. Required string.
- **title** – New title to assign to the session. Required string.

### Output
```javascript
{
  success: true,
  message: 'Session title edited succesfully',
  data: {
    id: 'session id',
    title: 'new title name',
    isTitleEdit: true,
    userId: 'user id',
    cid: 'cid string',
    metahash: 'hash string',
    personalityId: 'personality id',
    createdAt: 'timestamp',
    updatedAt: 'timestamp'
  }
}
```