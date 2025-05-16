# TwinProtocol Streaming Guide

This guide will walk you through the process of setting up a **real-time streaming connection** using the **TwinProtocol** package. The process consists of **4 steps**:

1. Setup a Stream Connection
2. Send SDP Answer to Establish Connection
3. Send ICE Candidate Data
4. Start the Stream

## Initialization

Prior to any implementation, it is necessary to initiate the package:

```javascript
import TwinProtocol from "twin-protocol-prod";
import dotenv from "dotenv";
dotenv.config();

class SampleClass {
  constructor() {
    this.twinProtocol = new TwinProtocol({
      TP_ACCESS_KEY: process.env.TP_ACCESS_KEY,
      TP_SECRET_KEY: process.env.TP_SECRET_KEY,
      TP_CLIENT_ID: process.env.TP_CLIENT_ID,
      TP_BASE_URL: process.env.TP_BASE_URL,
      TP_WS_URL: process.env.TP_WS_URL,
    });
  }

  /*package function implementations here */
}
```

## Step 1: Setup a Stream Connection

The first step is to initialize a **new stream session** for a Twin.

### Package function being used:

`setupConnection`

### Request Body Example:

```json
{
  "twinId": "your_twin_id",
  "responseResolution": your_resolution in integer
}
```

### Response Example:

```json
{
  "id": "your_stream_id",
  "offer": {
    /*other necessary data*/
  },
  "ice_servers": [
    /*other necessary data*/
  ],
  "session_id": "your_session_id"
}
```

### Sample Backend Implementation:

```javascript
async setupConnection(twinId, responseResolution) {
  try {
    const response = await this.twinProtocol.setupConnection(twinId, responseResolution);
    return response;
  } catch (error) {
    throw new Error(error.message);
  }
}
```

## Step 2: Send SDP Answer to Establish Connection

Once the stream connection is set up, the **client must send an SDP answer** to establish a WebRTC session.

### Package function being used:

`startConnection`

### Request Body Example:

```json
{
  "streamId": "your_stream_id",
  "answer": "your_sdp_answer",
  "sessionId": "your_session_id"
}
```

### Response Example:

```json
{
  "session_id": ""
}
```

### Sample Backend Implementation:

```javascript
async startConnection(streamId, answer, sessionId) {
  try {
    const response = await this.twinProtocol.startConnection(streamId, answer, sessionId);
    return response;
  } catch (error) {
    throw new Error(error.message);
  }
}
```

## Step 3: Send ICE Candidate Data

To ensure a smooth WebRTC connection, the **client must send ICE candidates** to establish network connectivity.

### Package function being used:

`sendNetworkInfo`

### Request Body Example:

```json
{
  "streamId": "your_stream_id",
  "sessionId": "your_session_id",
  "candidate": "candidate_string",
  "sdpMid": "sdp_mid",
  "sdpMLineIndex": integer
}
```

### Response Example:

```json
{
  "status": "created",
  "session_id": ""
}
```

### Sample Backend Implementation:

```javascript
async sendNetworkInfo(streamId, sessionId, candidate, sdpMid, sdpMLineIndex) {
  try {
    const response = await this.twinProtocol.sendNetworkInfo(streamId, sessionId, candidate, sdpMid, sdpMLineIndex);
    return response;
  } catch (error) {
    throw new Error(error.message);
  }
}
```

## Step 4: Start the Stream

Once the WebRTC connection is established, the **client can start streaming content**.

### Package function being used:

`startStream`

### Request Body Example:

```json
{
  "streamId": "your_stream_id",
  "twinId": "your_twin_id",
  "input": "text",
  "sessionId": "your_session_id"
}
```

### Response Example:

```json
{
  "status": "started",
  "video_id": ""
}
```

### Sample Backend Implementation:

```javascript
async startStream(streamId, input, twinId, sessionId) {
  try {
    const response = await this.twinProtocol.startStream(streamId, input, twinId, sessionId);
    return response;
  } catch (error) {
    throw new Error(error.message);
  }
}
```

## Delete Stream:

This functionality is used to close the connection and terminate the session. 

```javascript
const main = async () => {
  try {
    let streamId = ""; //provide the stream id here
    let sessionId = ""; //provide the session id here
    const resp = await twinProtocol.deleteStream(streamId, sessionId);
    console.log(resp);
  } catch (error) {
    console.error(error.message);
  }
};

main();
```
