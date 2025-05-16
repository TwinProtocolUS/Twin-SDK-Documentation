# Create Vault ID 

This document provides a guide on how to create a **Vault ID** for a user, based on their email and the platform they are registered on.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const email = "";
    const platformId = "";
    const resp = await twinProtocol.createVaultId(email, platformId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
email – The email address of the user for whom you want to create a vault ID. This is a required string parameter.

platformId – The unique identifier of the platform on which the user is registered. This is a required string parameter.

### Output
```javascript
{
  success: true,
  message: 'Vault Id and OTP sent to your email',
  data: null
}
```