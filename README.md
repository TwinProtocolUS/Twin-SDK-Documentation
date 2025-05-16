# Installation and Initialization

Prior to using any of the functionalities of the twin protocol package, it is necessary to install it, and then initialize in any file where its use case lies.

```bash
$ npm install twin-protocol-prod
```

## Configure environment variables

```bash
TP_ACCESS_KEY=
TP_SECRET_KEY=
TP_CLIENT_ID=
TP_BASE_URL=
TP_WS_URL=
```

## Usage

### Initialization

Steps to initialize the SDK:

```javascript
import TwinProtocol from "twin-protocol-prod";

const twinProtocol = new TwinProtocol({
  TP_ACCESS_KEY: "your-access-key",
  TP_SECRET_KEY: "your-secret-key",
  TP_CLIENT_ID: "your-client-id",
  TP_BASE_URL: "your-base-url",
  TP_WS_URL: "your-ws-url",
});

```