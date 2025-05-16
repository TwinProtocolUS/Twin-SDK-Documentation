# Get Average Session Time 

This document provides a guide on how to **get the average chat session time** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const resp = await twinProtocol.getAverageSessionTime();

    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};
main();
```

### Parameters

This function does not require any parameters.

### Output
```javascript
{
  success: true,
  message: 'Average session time retrieved successfully',
  data: 'H hours, M minutes, S seconds'
}
```