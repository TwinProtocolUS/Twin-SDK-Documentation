# Session History 

This document provides a guide on how to **get chat session history** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const sessionId = "your_session_id_here";
    const resp = await twinProtocol.sessionHistory(sessionId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **sessionId** – ID of the session whose history is to be retrieved. Required string.


### Output
```javascript
{
  success: true,
  message: 'Session History Fetched',
  data: { 
    history: ['array of all chat history objects here'] 
    }
}
```