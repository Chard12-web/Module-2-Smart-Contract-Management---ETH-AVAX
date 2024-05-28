# My First dApp

This is a decentralized application (dApp) built on Ethereum blockchain. It allows users to set and get their mood using a smart contract.

# Video link here 

https://www.loom.com/share/40661d3a90da45ce96f7e3a072335c37?sid=93dce5bd-5c19-4999-b2d5-26343853c01d

## Features

- Set your mood: Users can set their mood using the provided input field and button.
- Get your mood: Users can retrieve their mood previously set using the provided button.

## How to Use

1. Ensure you have a compatible Ethereum wallet (like MetaMask) installed in your browser.
2. Connect your wallet to the dApp.
3. Set your mood by typing it in the input field and clicking "Set Mood" button.
4. Retrieve your mood by clicking the "Get Mood" button.

## Installation

No installation is needed for the dApp. Simply open the provided HTML file in a web browser with MetaMask or any compatible Ethereum wallet extension installed.

## Development

- HTML, CSS, and JavaScript are used for the frontend.
- ethers.js library is used to interact with the Ethereum blockchain.
- Smart contract is deployed on Ethereum network with the provided address and ABI.

## Smart Contract

The smart contract used by this dApp is responsible for storing and retrieving user mood.

## Code 

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My First dApp</title>
  <style>
    body {
      text-align: center;
      font-family: Arial, Helvetica, sans-serif;
    } 

    div {
      width: 20%;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
    }

    button {
      width: 100%;
      margin: 10px 0px 5px 0px;
    }
  </style>
</head>

<body>
  <div>
    <h1>This is my dApp!</h1>
    <p>Here we can set or get the mood:</p>
    <label for="mood">Input Mood:</label> <br />
    <input type="text" id="mood" />
    <button id="getMoodButton" onclick="getMood()">Get Mood</button>
    <button onclick="setMood()">Set Mood</button>
  </div>

  <script src="https://cdn.ethers.io/lib/ethers-5.2.umd.min.js" type="application/javascript"></script>
  <script>
    const provider = new ethers.providers.Web3Provider(window.ethereum);

    const MoodContractAddress = "0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266";
    const MoodContractABI = [
      {
        "inputs": [
          {
            "internalType": "string",
            "name": "_mood",
            "type": "string"
          }
        ],
        "name": "setMood",
        "outputs": [],
        "stateMutability": "nonpayable",
        "type": "function"
      },
      {
        "inputs": [],
        "name": "getMood",
        "outputs": [
          {
            "internalType": "string",
            "name": "",
            "type": "string"
          }
        ],
        "stateMutability": "view",
        "type": "function"
      }
    ];

    let MoodContract;
    let signer;

    provider.send("eth_requestAccounts", []).then(() => {
      provider.listAccounts().then(function (accounts) {
        signer = provider.getSigner(accounts[0]);
        MoodContract = new ethers.Contract(
          MoodContractAddress,
          MoodContractABI,
          signer
        );
      });
    });

    async function getMood() {
      if (typeof window.ethereum !== "underfined") {
        await ethereum.request({method: "eth_requestAccounts"})
      }
    }

    async function setMood() {
      const mood = document.getElementById("mood").value;
      const setMoodPromise = MoodContract.setMood(mood);
      await setMoodPromise;
    }


  </script>
</body>

</html>
````
## Contributors

- [Richard](@Chard12) - Developer
