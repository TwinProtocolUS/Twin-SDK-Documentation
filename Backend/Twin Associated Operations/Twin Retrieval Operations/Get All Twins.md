# Get All Twins 

This document provides a guide on how to fetch all twins stored in the database, with support for pagination.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const page = 1;
    const limit = 10;
    const resp = await twinProtocol.getAllTwins({ page, limit });
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameters
page – The page number to retrieve. This is used to skip over earlier results.

limit – The number of results to return per page.

### Output
```javascript
{
  success: true,
  message: 'Twins fetched successfully.',
  data: {
    twins: ['array of twin recrods'],
    totalRecords: "count",
    currentPage: "page number",
    totalPages: "page count"
  }
}
```