# Fetch Twin Connectivity Requests

This document provides a guide on how to fetch all the connection requests received any platform for a specific twin, including the names of the brains (categories) and their current status.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const twinId = "";
    const categoryId = ""; // optional, leave blank to get all requests
    const resp = await twinProtocol.getConnectionRequests(twinId, categoryId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
twinId – Provide the unique identifier of the twin for which you want to fetch connection requests.

categoryId – (optional) Provide the category ID to filter the connection requests by a specific brain (category). If omitted, all requests for the given twin will be fetched.

### Output
```javascript
{
  success: true,
  message: 'Connection requests fetched successfully.',
  data: [ { twinName: '', categoryName: '', status:' pending/accepeted/rejected' } ]
}
```