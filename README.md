# Installation and Initialization

Prior to using any of the functionalities of the twin protocol package, it is necessary to install it, and then initialize in any file where its use case lies.

Depending on the instance your currently using (development/staging/production), install the package pointing to it:

```bash
#(development instance)
$ npm install twin-protocol-dev
```

```bash
#(staging instance)
$ npm install twin-protocol-staging
```

```bash
#(production instance)
$ npm install twin-protocol-prod
```

All the environment variable values listed below can be found on the twin platform's **Client Admin Portal**. To view the same, login using your credentials, then go to the **Configurations** menu from the left panel, and then choose the **Development** tab.

## Configure environment variables

```bash
TP_ACCESS_KEY=
TP_SECRET_KEY=
TP_CLIENT_API_KEY=
TP_BASE_URL=
TP_WS_URL=
```

## Usage

### Initialization

Steps to initialize the SDK:

```javascript
//depending on the instance in use (development, staging, production), make changes accordingly (ie, dev/staging/prod as the suffix for package name)
import TwinProtocol from "twin-protocol-dev/staging/prod";

const twinProtocol = new TwinProtocol({
  TP_ACCESS_KEY: "your-access-key",
  TP_SECRET_KEY: "your-secret-key",
  TP_CLIENT_API_KEY: "your-client-api-key",
  TP_BASE_URL: "your-base-url",
  TP_WS_URL: "your-ws-url",
});

```