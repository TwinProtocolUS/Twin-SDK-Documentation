# Import Vault 

This document provides a guide on how to **import** a previously created Vault ID from another platform to the specified platform, allowing the user to avoid creating unnecessary multiple Vault IDs for different platforms.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const vaultId = "";
    const platformId = "";
    const resp = await twinProtocol.importVault(vaultId, platformId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

## Parameters
vaultId – The unique identifier of the Vault ID that has already been created on another platform. This is a required string parameter.

platformId – The unique identifier of the platform to which the Vault ID is being imported. This is a required string parameter.

## Output
```javascript
{
  success: true,
  message: 'Vault Id and OTP sent to your email',
  data: {
     email: '' 
    }
}
```
