# Verify OTP 

This document provides a guide on how to **verify** the OTP (One-Time Password) for the creation of a vault ID by the user.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const email = "";
    const otp = "";
    const resp = await twinProtocol.verifyOtp(email, otp);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
email – The email address associated with the vault ID creation. This is a required string parameter.

otp – The One-Time Password (OTP) sent to the user for verifying vault ID creation. This is a required string parameter.


### Output
```javascript
{
  success: true,
  message: 'OTP verified successfully',
  data: {
    vaultId: ''
  }
}
```
