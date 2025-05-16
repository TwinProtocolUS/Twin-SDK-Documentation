# Delete Session 

This document provides a guide on how to **delete a chat session** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const sessionId = "your_session_id_here";

    const resp = await twinProtocol.deleteSession(sessionId);

    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **sessionId** – ID of the session to be deleted. Required string.


### Output
```javascript
{
  success: true,
  message: 'Session deleted successfully',
  data: []
}
