# Get All Personalities 

This document provides a guide on how to **get a list of all personalities** using the SDK.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const resp = await twinProtocol.getAllPersonalities();
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
  message: "Personalities fetched successfully.",
  data:{
    [
     {
      id: 'personality id',
      name: 'pesronality name',
      category: 'personality category',
      description: 'personality description',
      avatarImg: 'image url of personality',
      brainId: 'brain id',
      createdAt: 'timestamp',
      updatedAt: 'timestamp',
      gender: 'gender of the personality',
      url: 'social urls'
    },
         {
      id: 'personality id',
      name: 'pesronality name',
      category: 'personality category',
      description: 'personality description',
      avatarImg: 'image url of personality',
      brainId: 'brain id',
      createdAt: 'timestamp',
      updatedAt: 'timestamp',
      gender: 'gender of the personality',
      url: 'social urls'
    }
    ..."continued till the end of list"
  ]
}
}
```
