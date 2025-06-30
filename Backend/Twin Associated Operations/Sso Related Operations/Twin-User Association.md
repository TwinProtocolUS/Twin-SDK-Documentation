# Twin User Creation

This document provides a guide on how to map a User to a specific Twin, thus making it the user's default twin, or in other words, making the specified user the 'owner' of that Twin.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    let payload = {
      email: "", // email of the user whose mapping is to be done against a twin
      twinId: ""
    }
    const resp = await twinProtocol.associateTwinToUser(payload);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Output
```javascript
{
  success: true,
  message: 'Twin associated with user successfully',
  data: {
    email: '',
    twinId: '',
    twinName: ''
  }
}
```