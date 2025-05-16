# User Creation 

This document provides a guide on how to **create a user** using the SDK. This is the first step to do

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const resp = await twinProtocol.userWithMemory();
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

- This function does not require any parameters.


### Output
```javascript
{
  success: true,
  message: 'User with memory created successfully',
  data: {
    id: 'user id',
    createdAt: 'timestamp',
    updatedAt: 'timestamp',
    memoryBlocks: [ [Object] ]
  }
}
```