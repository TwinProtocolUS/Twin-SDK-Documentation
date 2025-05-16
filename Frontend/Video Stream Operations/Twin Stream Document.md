# TWIN Stream 

This document provides a guide on how to implement twin streaming in your application using TWIN Protocol's API.

## Overview

TWIN Stream allows you to integrate real-time AI avatar communication in your application. The implementation uses WebRTC for high-quality, low-latency video streaming of digital twins.

## Prerequisites

- Node.js and npm/yarn/bun
- Basic understanding of React and WebRTC
- Twin ID from the TWIN Protocol platform

## Getting Started

### Installation

```bash
npm install axios
```

### API Endpoints

The API is hosted at: `https://temp-stream-production.up.railway.app`

### Core Functionality

The implementation requires several steps to establish a WebRTC connection and stream a twin:

1. Set up the connection
2. Exchange ICE candidates
3. Start the connection
4. Start the stream with user input

## Implementation Guide

### 1. Setting Up the Connection

Create a function to set up the initial connection with the server:

```typescript
import axios from "axios";

const API_URL = "https://temp-stream-production.up.railway.app";

interface StreamData {
  id: string;
  session_id: string;
  offer: RTCSessionDescription;
  ice_servers: RTCIceServer[];
}

const setupConnection = async (
  twinId: string,
  resolution = 512
): Promise<StreamData> => {
  try {
    const res = await axios.post(
      `${API_URL}/v1/stream-package/setupConnection`,
      {
        twinId,
        responseResolution: resolution,
      }
    );

    if (!res?.data?.id || !res?.data?.session_id) {
      throw new Error("Invalid response from server");
    }

    return res.data;
  } catch (error) {
    console.error("Error setting up connection:", error);
    throw error;
  }
};
```

### 2. Managing ICE Candidates

Create a function to send ICE candidates to the server:

```typescript
const sendIceCandidate = async (
  streamId: string,
  sessionId: string,
  candidate?: RTCIceCandidate
): Promise<void> => {
  try {
    if (candidate) {
      const { candidate: candidateStr, sdpMid, sdpMLineIndex } = candidate;
      await axios.post(`${API_URL}/v1/stream-package/sendNetworkInfo`, {
        streamId,
        sessionId,
        candidate: candidateStr,
        sdpMid,
        sdpMLineIndex,
      });
    } else {
      // Signal ICE gathering complete
      await axios.post(`${API_URL}/v1/stream-package/sendNetworkInfo`, {
        streamId,
        sessionId,
      });
    }
  } catch (error) {
    console.error("Error sending ICE candidate:", error);
    throw error;
  }
};
```

### 3. Starting the Connection

Create a function to send the WebRTC answer to the server and start the connection:

```typescript
const startConnection = async (
  streamId: string,
  sessionId: string,
  answer: RTCSessionDescriptionInit
): Promise<void> => {
  try {
    await axios.post(`${API_URL}/v1/stream-package/startConnection`, {
      streamId,
      sessionId,
      answer,
    });
  } catch (error) {
    console.error("Error starting connection:", error);
    throw error;
  }
};
```

### 4. Initiating the Stream with User Input

Create a function to start streaming with user-provided input:

```typescript
const startStream = async (
  streamId: string,
  sessionId: string,
  input: string,
  twinId: string
): Promise<void> => {
  try {
    await axios.post(`${API_URL}/v1/stream-package/startStream`, {
      streamId,
      sessionId,
      input,
      twinId,
    });
  } catch (error) {
    console.error("Error starting stream:", error);
    throw error;
  }
};
```

### 5. WebRTC Implementation

Create a custom hook or component to handle the WebRTC connection:

```typescript
const createPeerConnection = async (
  streamData: StreamData
): Promise<RTCSessionDescriptionInit> => {
  try {
    const { offer, ice_servers: iceServers } = streamData;

    // Create RTCPeerConnection
    const pc = new RTCPeerConnection({
      iceServers,
      iceCandidatePoolSize: 10,
      bundlePolicy: "max-bundle",
    });

    // Create data channel
    const dataChannel = pc.createDataChannel("JanusDataChannel", {
      ordered: true,
      maxRetransmits: 3,
    });

    // Handle ICE connection state changes
    pc.oniceconnectionstatechange = () => {
      console.log("ICE Connection State:", pc.iceConnectionState);
      // Update UI based on connection state
    };

    // Handle ICE candidates
    pc.onicecandidate = async (event) => {
      try {
        await sendIceCandidate(
          streamData.id,
          streamData.session_id,
          event.candidate || undefined
        );
      } catch (error) {
        console.error("Error sending ICE candidate:", error);
      }
    };

    // Handle incoming tracks
    pc.ontrack = (event) => {
      console.log("Received track:", event.track.kind);

      // Track state monitoring
      event.track.addEventListener("ended", () => {
        console.log("Track ended:", event.track.kind);
      });

      const stream = event.streams[0];

      // Set the stream to your video element
      if (videoElement && stream) {
        videoElement.srcObject = stream;
        videoElement.onloadedmetadata = () => {
          videoElement.play().catch((error) => {
            console.warn("Auto-play prevented:", error);
          });
        };
      }
    };

    // Set remote description (the offer from the server)
    await pc.setRemoteDescription(offer);

    // Create answer
    const answer = await pc.createAnswer();
    await pc.setLocalDescription(answer);

    return answer;
  } catch (error) {
    console.error("Error creating peer connection:", error);
    throw error;
  }
};
```

### 6. Complete Implementation Flow

```typescript
// 1. Set up connection and get stream data
const streamData = await setupConnection(twinId);

// 2. Create peer connection and get answer
const answer = await createPeerConnection(streamData);

// 3. Start connection with the answer
await startConnection(streamData.id, streamData.session_id, answer);

// 4. Start streaming with user input
await startStream(
  streamData.id,
  streamData.session_id,
  "Hello, this is my message for the twin!",
  twinId
);
```

## React Component Example

Here's a simplified React component that implements twin streaming:

```jsx
import React, { useEffect, useRef, useState } from "react";
import {
  setupConnection,
  startConnection,
  startStream,
} from "../services/connectionService";

const TwinStreamComponent = ({ twinId }) => {
  const [streamData, setStreamData] = useState(null);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState(null);
  const [userInput, setUserInput] = useState("");
  const videoRef = useRef(null);
  const peerConnectionRef = useRef(null);

  // Initialize connection
  useEffect(() => {
    const initConnection = async () => {
      try {
        setIsLoading(true);
        const data = await setupConnection(twinId);
        setStreamData(data);
        await initializePeerConnection(data);
      } catch (err) {
        setError("Failed to establish connection");
        console.error(err);
      } finally {
        setIsLoading(false);
      }
    };

    initConnection();

    return () => {
      if (peerConnectionRef.current) {
        peerConnectionRef.current.close();
      }
    };
  }, [twinId]);

  // Initialize WebRTC peer connection
  const initializePeerConnection = async (data) => {
    try {
      const pc = new RTCPeerConnection({
        iceServers: data.ice_servers,
        iceCandidatePoolSize: 10,
      });

      pc.onicecandidate = (event) => handleIceCandidate(event, data);
      pc.ontrack = handleTrack;

      await pc.setRemoteDescription(data.offer);
      const answer = await pc.createAnswer();
      await pc.setLocalDescription(answer);

      peerConnectionRef.current = pc;

      await startConnection(data.id, data.session_id, answer);
    } catch (err) {
      setError("Failed to initialize WebRTC connection");
      console.error(err);
    }
  };

  // Handle ICE candidates
  const handleIceCandidate = async (event, data) => {
    if (event.candidate) {
      try {
        await sendIceCandidate(data.id, data.session_id, event.candidate);
      } catch (err) {
        console.error("Error sending ICE candidate:", err);
      }
    }
  };

  // Handle incoming tracks
  const handleTrack = (event) => {
    if (videoRef.current && event.streams && event.streams[0]) {
      videoRef.current.srcObject = event.streams[0];
    }
  };

  // Send message to twin
  const handleSendMessage = async () => {
    if (!userInput.trim() || !streamData) return;

    try {
      setIsLoading(true);
      await startStream(
        streamData.id,
        streamData.session_id,
        userInput,
        twinId
      );
    } catch (err) {
      setError("Failed to start stream");
      console.error(err);
    } finally {
      setIsLoading(false);
    }
  };

  return (
    <div>
      <div className="video-container">
        <video ref={videoRef} autoPlay playsInline />
      </div>

      {error && <div className="error-message">{error}</div>}

      <div className="input-container">
        <textarea
          value={userInput}
          onChange={(e) => setUserInput(e.target.value)}
          placeholder="Enter your message for the twin..."
        />
        <button onClick={handleSendMessage} disabled={isLoading || !streamData}>
          {isLoading ? "Sending..." : "Send Message"}
        </button>
      </div>
    </div>
  );
};

export default TwinStreamComponent;
```

## Important Notes

1. **Twin ID**: You need a valid twin ID to use this API. These can be obtained from the TWIN Protocol platform.

2. **Resolution**: You can specify the video resolution when setting up the connection (default is 512).

3. **Connection States**: Handle different connection states to provide a smooth user experience:

   - disconnected
   - loading
   - ready
   - live
   - ended

4. **Error Handling**: Implement robust error handling for network issues, connection failures, and API errors.

5. **Auto-play Issues**: Some browsers may block auto-play of video elements. Implement user-initiated play as a fallback.

## Troubleshooting

- **Connection Issues**: Ensure your ICE candidates are being properly sent and that your network allows WebRTC connections.
- **Video Not Displaying**: Check if the video element is properly receiving and displaying the MediaStream.
- **Twin Not Responding**: Verify that you're using a valid twin ID and that your input message is being properly sent.

## Additional Resources

For more information about the TWIN Protocol and API documentation, visit the official TWIN Protocol website.