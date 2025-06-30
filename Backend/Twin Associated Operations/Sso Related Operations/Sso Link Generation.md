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

## Note
Important Step:

To use the SSO link on the Twin front-end staging environment, you need to switch to your designated client instance. This is a one-time setup, as the selected client will be saved in local storage. Please note that the SSO link may not function properly in incognito mode.

For the production environment, once your white-label client is live, no additional configuration will be required. Everything will work smoothly for users without any extra steps.