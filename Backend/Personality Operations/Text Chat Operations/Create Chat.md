# Create Chat 

This document provides a guide on how to **create a new text chat** within an existing session between a user and a personality.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const sessionId = "session_123";
    const message = "Hello!";
    const userId = "user_456";
    const personalityId = "personality_789";
    const wordLimit = 100; //optional (set to 50 by default)
    const modelName = "gpt-4"; //optional (set to gpt-4 by default)
    const language = "en";  //optional (set to english by default)
    
    const resp = await twinProtocol.createChat(
      sessionId,
      message,
      userId,
      personalityId,
      wordLimit,
      modelName,
      language
    );
    
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- **sessionId** – The ID of the session to create the chat in. This is a required string parameter.
- **message** – The message content to send. This is a required string parameter.
- **userId** – The ID of the user sending the message. This is a required string parameter.
- **personalityId** – The ID of the personality to chat with. This is a required string parameter.
- **wordLimit** – Maximum word count for the response. This is an optional number parameter.
- **modelName** – The name of the model to use. This is an optional string parameter.
- **language** – The language code for the conversation. This is an optional string parameter.

### Output
```javascript
{
  success: true,
  message: 'Chat created successfully',
  data: 'String response'
}
```