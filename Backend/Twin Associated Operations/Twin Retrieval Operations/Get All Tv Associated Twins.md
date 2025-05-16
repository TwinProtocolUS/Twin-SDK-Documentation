# Get All Twin-TV 

This document provides a guide on how to **fetch all twins** that are available and linked to the TwinTV platform.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const resp = await twinProtocol.getAllTwinsTV();
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
  message: 'Twins-TV fetched successfully.',
  data: [
    {
      personalityName: '',
      avatar: '',        
      profession: '',
      description: '',
      personalityId: ''
    },
    {
      personalityName: '',
      avatar: '',     
      profession: '',
      description: '',
      personalityId: ''
    }

    '...till end of list'
  ]
}
```