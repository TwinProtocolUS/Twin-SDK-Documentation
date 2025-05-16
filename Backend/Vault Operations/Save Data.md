# Save Data 

This document provides a guide on how to **store structured data into the Vault**, typically related to user interactions, assets, or knowledge inputs.

## After installing and initializing the package:

```javascript
const main = async () => {
  try {
    const vaultId = "";     
    const cid = "";         
    const sessionId = "";
    const dataType = "";     
    const brainId = "";     
    const assets = null;     
    const assestsUrl = null;  
    const twinId = null;       
    const tokenId = null;     
    const name = null;        
    const description = null; 

    const resp = await twinProtocol.saveData(
      vaultId,
      cid,
      sessionId,
      dataType,
      brainId,
      assets,
      assetsUrl,
      twinId,
      tokenId,
      name,
      description
    );

    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```

## Parameters
vaultId (string, required): ID of the vault where the data will be stored.

cid (string, required): Unique content identifier for the data.

sessionId (string, optional): Session reference for grouping data.

dataType (string, required): Specifies the type of data (e.g., "text", "audio").

brainId (string, required): The brain ID to which this data is relevant.

assets (any, optional): Additional media or data assets.

assetsUrl (string, optional): URL pointing to asset location.

twinId (string, optional): ID of the associated twin.

tokenId (string, optional): Optional token reference.

name (string, optional)

description (string, optional)

## Output
```javascript
{ 
  success: true, 
  message: 'Data saved successfully', 
  data: null
}
```