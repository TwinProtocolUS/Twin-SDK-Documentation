# Create Personality 

This document provides a guide on how to **create a personality of a twin** using the SDK.

## After installing and initializing the package:

```javascript

const main = async () => {
    try {

      // to upload a file with text specified in code editor itself
      const fileBuffer = Buffer.from("This part is for testing sample text file upload from the code file itself", "utf-8");

      const bufferToStream = (buffer) => {
          const stream = new Readable();
          stream._read = () => { };
          stream.push(buffer);
          stream.push(null);
          return stream;
      };

        const formData = new FormData();

        // to upload a file from the available locally
        const filePath = path.join(process.cwd(), "file path for the locally available file goes here");

        formData.append("files", fs.createReadStream(filePath));
        formData.append("name", "Personality's name goes here");
        formData.append("category", "The category name(eg: Healthcare, AI etc.) goes here");             // optional
        formData.append("brainId", "");                                                                  // optional
        formData.append("description", "File/category description goes here");                           // optional
        formData.append("gender", "");                                                                   // optional
        formData.append("url", "A social url, such as linkedin profile, goes here");                     // optional
        formData.append("avatarImg", "base 64 string OR live link (hosted url) for the image goes here") // optional
        formData.append("webhookUrl", "Webhook url goes here");                                          // optional

        /* Note: The file ingestion process on Persona LLM is asynchronous. 
           As a result, uploaded files may take some time before their status is marked as "successfully ingested". 
           To reliably track the status of uploaded training files, it is recommended to provide a custom webhook URL.
           This ensures you are notified when ingestion completes or fails.
           Without this, if you attempt to use the createChat functionality (refer to Personality Operations/Text Chat Operations/Create Chat)
           before the files are fully ingested, you may encounter incomplete or invalid responses. */
        
        // sample webhook response: 
           {
              "personalityId": "",
              "status": true,
              "message": "File ingested successfully.",
              "fileName": ""
           } 

        const fileStream = bufferToStream(fileBuffer);
        formData.append("files", fileStream, {
            filename: "The name of the file goes here (.txt/pdf/doc)",
            contentType: "text/plain",
        });

        const resp = await twinProtocol.createPersonality(formData);
        console.log(resp);
    } catch (error) {
        console.error(error.message);
    }
};
main();
```

### Parameters

- **formData** –  Form data containing personality details like name, URL, description, etc. Required object.


### Output
```javascript
{
  success: true,
  message: 'Personality created successfully',
  data: {
    personalityId: '',
    name: '',
    brainId: '',
    createdAt: ''
  }
}
```
