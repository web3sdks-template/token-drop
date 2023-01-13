# Token Drop Example

## Introduction

In this guide, we will utilize the [**Token Drop**](https://docs.web3sdks.com/contracts/token-drop) contract to release ERC-20 tokens!

We also utilize the token drop's [claim phases](https://docs.web3sdks.com/pre-built-contracts/token-drop#setting-claim-phases) feature, to release the tokens for a price, and only allow a certain amount to be claimed per wallet.

**Check out the Demo here**: https://token-drop.web3sdks-template.com/

## Tools:

- [**web3sdks Token Drop**](https://docs.web3sdks.com/contracts/token-drop): web3sdks's Token Drop contract is a way of releasing your ERC20 tokens!

- [**web3sdks React SDK**](https://docs.web3sdks.com/react): To connect to our NFT Collection Smart contract via React hooks such as [useTokenDrop](https://docs.web3sdks.com/react/react.usetokendrop), connect user's wallets, and other awesome hooks like [useActiveClaimCondition](https://docs.web3sdks.com/react/react.useactiveclaimcondition) and [useClaimIneligibilityReasons](https://docs.web3sdks.com/react/react.useclaimineligibilityreasons).

- [**web3sdks TypeScript SDK**](https://docs.web3sdks.com/typescript): To claim/mint tokens from the token drop with [.claim](https://docs.web3sdks.com/pre-built-contracts/token-drop#claiming-tokens) , view token balance with [.balanceOf](https://docs.web3sdks.com/pre-built-contracts/token-drop#token-balance), and transfer tokens with [.transfer](https://docs.web3sdks.com/pre-built-contracts/token-drop#transfer-tokens).

## Using This Repo

- Create a Token Drop contract via the web3sdks dashboard on the Mumbai test network.

- Create a project using this example by running:

```bash
npx web3sdks create --template token-drop
```

- Replace our demo token drop contract address (`0x5ec440E5965da9570CAa66402980c6D20cbe0663`) with your token drop contract address!

# Guide

## Configuring the Web3sdksProvider

The web3sdks provider is a wrapper around our whole application.

It allows us to access all of the React SDK's helpful hooks anywhere in our application.

```jsx
// This is the chainId your dApp will work on.
const activeChainId = ChainId.Mumbai;

function MyApp({ Component, pageProps }) {
  return (
    <Web3sdksProvider desiredChainId={activeChainId}>
      <Component {...pageProps} />
    </Web3sdksProvider>
  );
}
```

## Connecting User's Wallets

We use the [useMetamask](https://docs.web3sdks.com/react/react.usemetamask) hook to connect with user's wallets.

```jsx
const connectWithMetamask = useMetamask();

// ...
<button onClick={connectWithMetamask}>Connect with Metamask</button>;
```

## Getting the token drop contract

We use the [useContract](https://docs.web3sdks.com/react/react.useContract) hook to get the token drop contract:

```jsx
const { contract: tokenDropContract } = useContract(
  "0x5ec440E5965da9570CAa66402980c6D20cbe0663",
  "token-drop"
);
```

## Claiming Tokens

We use the `claim` function and pass in the desired amount of tokens to claim inside a `Web3Button` component:

We store a value the user types into an input field in state:

```jsx
const [amountToClaim, setAmountToClaim] = useState("");

// ...

<div className={styles.claimGrid}>
  <input
    type="text"
    placeholder="Enter amount to claim"
    onChange={(e) => setAmountToClaim(e.target.value)}
    className={`${styles.textInput} ${styles.noGapBottom}`}
  />
  <Web3Button
    accentColor="#5204BF"
    colorMode="dark"
    contractAddress="0x5ec440E5965da9570CAa66402980c6D20cbe0663"
    action={(contract) => contract.erc20.claim(amountToClaim)}
    onSuccess={() => alert("Claimed!")}
    onError={(err) => alert(err)}
  >
    Claim Tokens
  </Web3Button>
</div>;
```

## Join our Discord!

For any questions, suggestions, join our discord at [https://discord.gg/cd web3sdks](https://discord.gg/KX2tsh9A).
