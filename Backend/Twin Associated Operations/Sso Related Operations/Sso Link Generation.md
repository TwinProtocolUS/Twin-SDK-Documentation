# SSO Link Generation

This document provides a guide on how to generate a single-sign-on link using a user's `email`.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    let payload = {
      email: "", // email of the user present in Twin Platform DB
      redirectPath: "" // optional (to specify a particular route/path appended at the end of the sso url)
    }
    const resp = await twinProtocol.generateSsoLink(payload);
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
  message: "SSO link generated successfully",
  data: {
    ssoLink: "<Base Url associated to the client(fetched via Twin Platform DB)>/sso-login?token=<Token Value>&redirectPath=/(optional)"
  }
}
```