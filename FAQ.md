# Frequently Asked Questions

Welcome to the iExec FAQ section. Here you'll find answers to common questions.

---
<details>
  <summary>Returned data is always a file</summary>
  
    The output it's a file and it's always be zipped with its content
    It's possible to push the output on a blockchain

</details>
<details>
  <summary>Is it possible to have encrypted output?</summary>
  
    Yes, this is possible through the SDK options.

</details>

<details>
  <summary>Where do the outputs land on IPFS?</summary>
  
    The data is dropped decrypted on IPFS, but it is also possible to store it encrypted on IPFS or Dropbox for instance

</details>

<details>
  <summary>Does encryption impact data organization and conversion?</summary>
  
    Normally, no. The iApp is responsible for handling this.

</details>

<details>
  <summary>Reverse lookup from an IPFS CID to the smart contract to find the data protector contract?</summary>
  
    Yes, it's possible to find the wallet, task and deal.

</details>
<details>
  <summary>Ability to look in the marketplace to add information for IP licensing?</summary>
  
    Yes, this is possible.

</details>

<details>
  <summary>Datapool processing?</summary>
  
    Planned for Q2.

</details>

<details>
  <summary>Will processing four megabytes be an issue in the TEE?</summary>
  
    It should be possible, we could make some stress test 

</details>

---

## 🔹 Issues with deploying smart contracts on Bellecour

### Problem  
iExec Sidechain “Bellecour” is a standard EVM-based sidechain dedicated to the iExec protocol. This article lists some of the things that can go wrong when one attempts to deploy smart contracts on IExec Sidechain Bellecour.

### Solution  
Possible causes and fixes :
- **Whitelisting Required**  
  Only whitelisted wallets can deploy contracts.  
  → [Request whitelisting via support ticket](https://iexecproject.atlassian.net/servicedesk/customer/portal/4/group/9/create/66)

- **Incorrect Wallet**  
  Verify you're using your whitelisted deployment wallet.

- **Gas Configuration**  
  - Set gas price to **0 Wei**
  - Ensure sufficient gas limit (minimum 2M recommended)


## 🔹 Error: Failed to Establish an Encrypted Channel to CAS

### Problem
When running a SCONE-based TEE Dapp, you might encounter the following error:
```
[SCONE|WARN] rust-cache/cargo/registry/src/github.com-1ecc6299db9ec823/rustls-0.19.1/src/session.rs:798:Sending fatal alert BadCertificate
[SCONE|FATAL] src/process/init.c:379:__scone_prepare_secure_config(): Could not initialize enclave state: Attestation failed
Caused by: Failed to establish an encrypted channel to CAS
Caused by: I/O error
Caused by: invalid certificate: UnknownIssuer 
```

### Solution  
This error happens when the image used to build the application does not match the CAS version set-up in the worker.
To solve the issue, please make sure that:
- You are building your Dapp using the latest version of the sconifier image
- You are following the instructions provided in the [documentation](https://protocol.docs.iex.ec/for-developers/confidential-computing/create-your-first-sgx-app).


## 🔹 Accessing the SCONE build tools

### Problem
You have requested access to the SCONE build tools via email but have not received a response, and the tools are not appearing on GitLab.

### Solution  
Access to the SCONE tools is typically granted within 2 to 24 hours. If you haven't received a reply after this period, it's advisable to contact the Scontain team again.


## 🔹 Docker Cleanup

### Problem
Guide to cleaning your local Docker environment , no space left on device
```
docker: Error response from daemon: no space left on device
```

### Solution  
To clean up Docker and remove unused images, the main command is ```docker image prune ```. For a more comprehensive cleanup that also includes unused containers and networks, use ```docker system prune```. If you want to delete all images not associated with a container, not just dangling ones, add the ```-a``` flag to these commands.


## 🔹 Buffer is not defined

### Problem
ReferenceError : "Buffer is not defined" on a vite project .

### Solution  
To solve the issue, configure a polyfill for Buffer by following this guide:  
[Buffer polyfill on StackOverflow](https://stackoverflow.com/questions/70714690/buffer-is-not-defined-in-react-vite)


## 🔹 Can I bridge RLC from a centralized exchange to The iExec Sidechain "Bellecour"?

### Problem
You are holding RLC on a centralized exchange (such as Binance, Kraken or Coinbase) and want to transfer some of your balance to iExec Sidechain “Bellecour” so you can use them with iExec, for example for requesting tasks.

### Solution  
The iExec sidechain “Bellecour” is an EVM-compatible chain that is only bridged to Ethereum Mainnet. iExec does not support direct transfers of funds from any centralized exchange to a wallet on Bellecour.
This means that to use your RLC balance on iExec Sidechain “Bellecour” you will need to first use the “Withdraw” feature of your exchange to transfer RLC to a wallet on Ethereum Mainnet, and then you can use the iExec bridge to transfer RLC from that wallet to your wallet on iExec Sidechain “Bellecour”.


## 🔹 CORS errors with The Graph

### Problem
The subgraph often responds with a CORS error, even though the actual issue might be something different, such as an invalid query or syntax errors in requests with The Graph.
```
Access to fetch at "x" from origin "y" has been blocked by CORS policy: Response to preflight request doesn't pass access control check:It does not have http ok status.
The GraphQL net::ERR_FAILED
```

### Solution  
Verify the syntax before further analysis, such as checking for missing curly braces, you can directly test the query on the following URL: [thegraph.bellecour.iex.ec](https://thegraph.bellecour.iex.ec/subgraphs/name/bellecour/poco-v5). This will allow you to quickly identify syntax errors.



## 🔹 Task processing is too long

### Problem
Users have reported a prolonged task processing time, with a minimum of 5 minutes, when working with the iExec Protocol.

### Solution  
**Explaination** 
- Order Matching :
  The system needs to meticulously match orders, considering various parameters, to ensure accuracy in task allocation.
- Docker Image Download :
  Retrieving the necessary Docker image for task execution is a critical step, and the time taken depends on the image size and network conditions.
- SGX Attestation Verification :
  Security is paramount, and the Dapp verifies the SGX attestation with Intel to ensure the integrity of the execution environment.
- Task Execution :
  The actual execution of the task involves complex computations, and the time taken is influenced by the nature and complexity of the task.
- Result Uploading :
  Once the task is executed, the results are uploaded, which can take time based on the size of the data and network conditions.
You can learn more about the task statuses in our documentation

**Future improvements**

We acknowledge the concerns regarding the extended processing time and want our users to know that we are actively working on optimizing the performance of the iExec Protocol. Here are some aspects we are currently addressing :
- PoCo Boost - On-Chain Protocol Optimization :
We're optimizing our on-chain protocol with PoCo Boost to reduce transactions and lower gas usage per deal. This aims to significantly improve transaction speed and cost-effectiveness.
- Intel Collaboration and Research :
Constant collaboration with Intel includes in-depth research to enhance SGX attestation processes, ensuring a more secure and efficient iExec Protocol.
- Language Benchmarking :
We're benchmarking worker processes across different code languages, aiming to identify the most efficient ones for specific tasks. This optimization contributes to overall Protocol performance.

## 🔹 Data Protector Access Issues

### Problem
Whitelist Contract Error

**Error Message:** "This whitelist contract address does not exist in the app whitelist registry"
### Solution
- Use whitelisted app addresses
- Default whitelisted app address: 0x256bcd881c33bdf9df952f2a0148f27d439f2e64
- For custom apps, they need to be whitelisted by the iExec team

### Problem
Collection Management Access

**Error Message:** "This collection can't be managed by you"
### Solution
- Only collection owners can manage their collections
- Users need proper permissions to add to collections
- Consider implementing a two-step collection management system:
  1. Users create their own collections
  2. Main collection owner grants access for adding to the primary collection

## 🔹 Protected Data Consumption Issues

### Problem
Workerpool Order Not Found

**Error Message:** "Could not find a workerpool order, maybe too many requests?"
### Solution
- Retry after a few minutes when computing resources become available
- This happens when the workerpool is at 100% capacity
- The error is temporary and related to resource availability

### Problem
Task Processing Stuck at 0%
### Solution
- Check if trying to consume the same data multiple times
- Verify data size and format
- Use the task debug feature to see detailed logs:
  ```bash
  iexec task debug [taskID]
  ```

## 🔹 Integration Issues
### Problem
CORS in Development

**Error Message:** "Access to fetch at 'https://ipfs-upload.v8-bellecour.iex.ec/api/v0/add' has been blocked by CORS policy"
### Solution
- Use the recommended IPFS gateway: https://ipfs-gateway.v8-bellecour.iex.ec
- For content creators, use: https://github.com/iExecBlockchainComputing/content-creator-usecase-demo/.env.prod

## 🔹 Next.js Integration Error
### Problem
**Error Message:** "Module parse failed: Unexpected token (808:63)"
### Solution
- Ensure proper initialization of DataProtector methods
- Don't just initialize the module, use specific methods like protectData()
- Reference the sandbox implementation: https://codesandbox.io/p/github/iexecblockchaincomputing/dataprotector-sandbox/main

## 🔹 Chain Support and Configuration
### Problem
Custom Chain Support

**Context:** Using DataProtector with different chains

### Solution
- DataProtector is built specifically for iExec sidechain
- Only supports https://bellecour.iex.ec
- Not compatible with other chains like Citrea
- Requires specific Web3 provider configuration:
```javascript
const web3Provider = new Web3.providers.HttpProvider('https://bellecour.iex.ec');
```

## 🔹 Best Practices and Workflows DPS

### Recommended Workflow for DataProtector Sharing:
1. Create a collection
2. Create Protected Data
3. Create AddOnlyAppWhitelist
4. Add Protected Data to collection
5. Set renting/selling/subscription parameters
6. Set Protected Data to renting/sale/subscription
7. Rent/Buy/Subscribe to Protected Data
8. Consume the Protected Data content

### Notes:
- Renting and subscription models are currently more reliable than purchase for data consumption
- All data added to collections is immutable
- Processing protected data requires proper access rights and available computing resources
- Test with price set to 0 if RLC tokens are not available


