# Get Twin By ID 

This document provides a guide on how to fetch a specific twin from the database using a given `twinId`.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const twinId = "";
    const resp = await twinProtocol.twinBasedOnId(twinId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

### Parameter
twinId – Provide the unique identifier of the twin you want to retrieve.

### Output
```javascript
{
  success: true,
  message: 'Twin fetched successfully.',
  data: {
    subscriptionDetails: { status: false },
    demoAccess: { questionsAsked: 0 },
    twinStudio: {
      expressStatus: null,
      expressId: null,
      requestedExpressId: null,
      expressService: boolean,
      standardService: boolean,
      status: boolean
    },
    isRequested: { status: boolean, packageId: '' },
    linkedInUrl: null,
    _id: '',
    name: '',
    profession: '',
    description: '',
    personalityName: '',
    audioData: [],
    cloneAudio: boolean,
    tags: [],
    status: boolean,
    clientId: '',
    userIds: [],
    createdBy: '',
    categoryData: [],
    toxicFilter: boolean,
    isFeatured: boolean,
    contextScope: boolean,
    dapVisibility: boolean,
    listOnShowroom: boolean,
    createdAt: '',
    updatedAt: '',
    __v: 1,
    avatar: '',
    voiceId: '',
    freeQuestions: number,
    pointPerQuestion: 1,
    imageAvatars: [ ['image urls'] ],
    expressAvatars: [],
    listOnTv: boolean,
    brainMappings: []
  }
}
```