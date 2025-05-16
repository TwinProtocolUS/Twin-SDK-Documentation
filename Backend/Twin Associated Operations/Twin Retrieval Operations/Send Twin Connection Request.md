# Create Twin Connectivity Request 

This document provides a guide on how to send a connection request for specific "brains" (categories) of a particular twin from a platform to the Twin Protocol platform.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const twinId = "";
    const categoryIds = [];
    const resp = await twinProtocol.createConnectionRequest(twinId, categoryIds);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
twinId – Provide the unique identifier of the twin for which the connection request is being sent.

categoryIds – Provide an array of category IDs (brains) for which the connection request is made. These categories represent the specific capabilities or data of the twin.

### Output/Function
```javascript
{
  success: true,
  message: 'Connection request(s) sent successfully.',
  data: [
    {
      twinName: '',
      twinDescription: '',
      categoryName: '',
      status: 'pending/accepted/rejected'
    }
  ]
}
```