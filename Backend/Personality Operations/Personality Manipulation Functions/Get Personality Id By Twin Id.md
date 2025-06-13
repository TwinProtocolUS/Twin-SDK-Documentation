# Get Personality ID By Twin ID 

This document provides a guide on how to fetch personality id(s) associated with a given `twinId`.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const twinId = "";
    const resp = await twinProtocol.getPersonalityIdsFromTwinId(twinId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameter
twinId – Provide the unique identifier of the twin whise personality ids you want to retrieve.

### Output
```javascript
{
  success: true,
  message: 'Personality IDs associated with the twin fetched successfully',
  data: {
    name: '',
    personalityName: '',
    profession: '',
    brainMappings: [
      [Object], [Object],
      [Object], [Object],
      [Object], [Object],
      [Object], [Object],
      [Object]
    ]
  }
}
```

**Note: Please make use of destructuring the response (resp.data.brainMappings) to see the actual values, which by default get displayed as object blocks in the console.