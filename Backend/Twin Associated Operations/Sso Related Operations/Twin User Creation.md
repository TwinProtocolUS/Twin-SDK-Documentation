# Twin User Creation

This document provides a guide on how to inject a user in Twin Platform DB directly via SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    let payload = {
      email: "", // email for which a DB entry record is to be made,
      password: "" // optional (by default, Twin Platform Generates a random password string)
    }
    const resp = await twinProtocol.createUser(payload);
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
  message: 'User onboarded successfully.',
  data: {
    clientId: '',
    personaUserId: '',
    email: '',
    password: '',
    subscriptionId: [],
    status: true,
    is2faEnabled: false,
    isreferred: false,
    twinIds: []
  }
}
```