# Twin User Existence Check

This document provides a guide on how to verify whether or not a user is registered on the Twin Protocol Platform.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const email = "" // email of the user whose existence in the Twin DB is to be checked
    const resp = await twinProtocol.checkUserExistence(email);
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
  message: 'User found',
  data: {
    clientId: '',
    personaUserId: '',
    email: '',
    subscriptionId: [],
    status: true,
    is2faEnabled: false,
    isreferred: false,
    twinIds: []
  }
}
```