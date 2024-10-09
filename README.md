## Running Node.js scripts on Apillon Cloud Functions

The provided TypeScript code snippet is a template for deploying a script to the [Acurast network](https://acurast.com/) through [Apillon](https://apillon.io/). This script is designed to establish a WebSocket connection to Acurast's decentralized network, which is essential for enabling communication between your script and the Acurast processors. Here's a breakdown of how this template works and how it fits into the deployment process:

### Code Explanation

```typescript:index.ts
declare const _STD_: any;

_STD_.ws.open(
  [
    "wss://websocket-proxy-1.prod.gke.acurast.com/",
    "wss://websocket-proxy-2.prod.gke.acurast.com/",
  ],
  () => {
    // Success callback: Code to execute when the WebSocket connection is successfully opened
  },
  (error) => {
    // Error callback: Code to handle any errors that occur while opening the WebSocket connection
  }
);
```

This template and deployment process allow you to leverage Acurast's decentralized infrastructure for running your Node.js scripts, ensuring they are accessible and callable through the Apillon gateway. For more detailed runtime environment documentation, you can refer to the [Acurast Developer Docs](https://docs.acurast.com/developers/deployment-runtime-environment).

- **`_STD_` Object**: This is a special object provided by the Acurast runtime environment. It exposes various functionalities, including WebSocket operations, environment variable access, and more.

- **WebSocket Connection**: The `ws.open` method is used to establish a connection to the Acurast network. The URLs provided are endpoints for the WebSocket proxies that facilitate communication with the network.

- **Callbacks**: The code includes placeholders for success and error callbacks. You can define what actions to take when the connection is successfully established or if an error occurs.

### Deployment Process

1. **Edit the Script**: You can modify the `index.ts` file and add additional files or folders as needed for your application logic.

2. **Environment Variables**: Access environment variables using `_STD_.env["APILLON_API_KEY"]`. This is crucial for securely managing sensitive information like API keys.

3. **Build the Script**:
   - Run `npm run i` to install dependencies.
   - Run `npm run build` to compile the TypeScript code into a JavaScript bundle (`index.bundle.js`).

4. **Deploy the Script**:
   - **Via Apillon Dashboard**: Upload the `index.bundle.js` file to the Apillon dashboard at [Apillon Cloud Functions](https://app.apillon.io/dashboard/service/cloud-functions/).
   - **Via API**: Alternatively, you can deploy the script using the Apillon API. Documentation for this process is available at [Apillon Web3 Cloud Functions](https://wiki-staging.apillon.io/web3-services/8-web3-cloud-functions.html) and [Apillon Cloud Functions API](https://wiki-staging.apillon.io/build/11-cloud-functions-api.html).

5. **Obtain Execution Endpoint**: After deploying, wait a few minutes. You will obtain the callable endpoint to execute the job on the Apillon dashboard.