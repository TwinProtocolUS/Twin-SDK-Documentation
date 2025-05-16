# Get Twin By Name 

This document provides a guide on how to retrieve twins from the database using a specific `personalityName`, with optional pagination.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const personalityName = "";
    const page = 1;
    const limit = 10;
    const resp = await twinProtocol.getTwinByName(personalityName, page, limit);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
personalityName – Provide the name of the personality associated with the twin(s) you want to search for. This is a required string parameter.

page – (optional) The page number to retrieve. Used for paginating results.

limit – (optional) The number of results to return per page.

### Output
```javascript
{
  success: true,
  message: 'Twin(s) fetched successfully.',
  data: {
    twins: [ ['array of twin record(s)'] ],
    totalRecords: number,
    currentPage: number,
    totalPages: number
  }
}
```