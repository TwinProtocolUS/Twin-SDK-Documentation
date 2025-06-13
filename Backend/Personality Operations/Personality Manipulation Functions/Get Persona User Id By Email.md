# Get Persona User ID By User's Email 

This document provides a guide on how to fetch persona userId for a given `email`.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const email = "";
    const resp = await twinProtocol.getPersonaUserIdByEmail(email);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameter
email – Provide the user's email id with which one has been registered on the Twin Platform.

### Output
```javascript
{
  success: true,
  message: 'Persona user ID fetched successfully.',
  data: { 
    personaUserId: '' 
    }
}
```
