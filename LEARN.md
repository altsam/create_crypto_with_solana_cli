# Creating Cryptocurrency using Solana CLI

Welcome to the create your crypto quest wherein you’ll be creating your first cryptocurrency on Solana. Solana is the fastest blockchain in the world which boasts sub-second transaction speeds.

By the end of this quest, you would’ve created your very own cryptocurrency (your personal token) in under 15 minutes! You can share these tokens with your friends for social clout, or use them for crowdfunding your next big project, the possibilities are endless!

There are a couple of things that should be set up in your local machine before we move on. First up, you need to have a functioning rust installation along with cargo.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Since we’ll be creating our tokens using a command-line interface(CLI), we recommend using any \*nix OS (Linux or Mac). Windows users can install WSL for running shell commands

## Installing Tools

The Solana blockchain offers something called as programs, which are functions that reside on the Solana blockchain that help in performing complex transactions over the blockchain. Solana natively has a set of Programs deployed for usage. These set of on-chain programs are collectively known as the Solana Program Library or the SPL. To interact with these programs, we’ll be using the solana-cli.
First, we need to install the Solana tool suite in our machine. To do so, run the following command.

```
sh -c "$(curl -sSfL https://release.solana.com/v1.7.12/install)"
```

To confirm that Solana has been installed successfully and added to your PATH, run

```
solana --version
```

Now, we’ll be installing the spl-token-cli, which is a rust package (called a crate) for interacting with the SPL Token program that’ll be used for creating our tokens. It can be installed by running the following command.

```
cargo install spl-token-cli
```

## Creating a wallet

The best thing about Solana and other blockchains is that they allow us to manage money very seamlessly. To transact money on the blockchain, you need to use a software that facilitates these transactions called a wallet. Crypto wallets are physical devices or virtual programs that allow us to easily store and retrieve our crypto assets i.e. any cryptocurrencies that we might have on the blockchain.

To set up the wallet, run the below command

```
solana-keygen new
```

Every wallet on the Solana blockchain has a unique identifier, called the public key (shortened as pubkey) which is a cryptographic string of alpha-numeric characters. This pubkey can be universally shared with anyone and acts as a “receiving address” for your wallet. To check the public key and the balance of our newly created wallet, use the following commands.

Apart from the public key, you also have something called the private key - which is again a cryptographic string of alpha-numeric characters. Your private key (which you shouldn't share with anyone) along with your public key (wallet address) is used to verify your identity on the Solana Blockchain.


![1_solana_keygen](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/1_solana_keygen.png)


To check the balance of your newly created wallet, you can simply type

```
solana balance
```

![2](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/2_solana_pubkey.png)


You can also verify this by pasting your public key on the solana explorer - https://explorer.solana.com/?cluster=devnet 

![2](https://github.com/AdityaSh91/create_crypto_with_solana_cli/raw/main/learn_assets/explorer_balance_check.png)

The original Solana blockchain where the actual transactions happen is known as the mainnet. To perform any transaction on the Solana blockchain, you’re charged a transaction fee. These payments happen in a currency called SOL.

Solana also maintains clusters called devnet and testnet. Devnet is the replica of the Solana’s mainnet, and serves as a playground for anyone who wants to try out the features of Solana. Cryptos that reside in devnet don’t have any value, and hence we can transfer some “toy SOL” to our wallet for performing any transaction that we want. This process of receiving some crypto currency without paying for it is known as “airdrop”.

Since we need some SOL in our wallet, we’ll be airdropping some on the devnet. To run commands over the devnet, we can just pass “--url https://api.devnet.solana.com/” to all of our commands.
To airdrop some tokens in your account, use the following command.

```
solana airdrop 1 <public key> --url https://api.devnet.solana.com
```


![3](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/3_solana_airdrop.png)
To check your new balance, run the following command
![4](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/4_solana_balance.png)


## Creating your own tokens

Before we move onto the next section, we must first discuss a bit about tokens and cryptocurrencies. Cryptocurrency refers to the native assets of a blockchain, i.e. the currency that is used to perform transactions in the blockchain. Popular examples include BTC for Bitcoin, ETH for ethereum and SOL for Solana. On the other hand, tokens are built on top of an existing blockchain and are implemented using smart contracts. To put it simply, they’re a tradeable asset that reside in the blockchain, and may or may not have a value.

Solana gives us many programs in it’s library by default for many of the standard tasks that we’d usually do on the Solana Blockchain. This is called the SPL library. One of the most powerful features of Solana is that it has native support for creating a token over its blockchain.
Our token is actually created by a smart contract (program) in the SPL library. This program is known as the “SPL token program” and is the program that is used to create our own tokens. We’ll be using the spl-token CLI to interact with this SPL token program.

We can create a token by running

```
spl-token create-token --url https://api.devnet.solana.com/
```


![5](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/5_solana_create_token.png)


We have now created our very first token! As mentioned earlier, tokens are created using the SPL smart contracts. These smart contracts have a unique address in the blockchain which is a string of alpha-numeric characters. The address of this smart contract that holds the logic for the token’s behaviour is known as the “token address”. For all the actions that we’ll be performing for our tokens such as minting, burning etc, we’ll be interacting with this smart contract and hence we need to note down the address of this smart contract.

Congratulations on creating your very own cryptocurrency! \( ﾟヮﾟ)/

## Minting new tokens

There can be hundred different types of tokens that you can own. In Solana wallets, to transact in a particular type of token, we need to have an “account” in the wallet that can hold that token. A wallet can have multiple accounts, and each account is used to transact in one type of token. For our wallet, we need to create an account that can hold our token. To do so, we can run the following command which will create an account for us in our wallet by simply giving the token address.

```
spl-token create-account <token address> --url https://api.devnet.solana.com
```


![6](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/6_solana_create_account.png)


In the above image ‘BghFzN668wXWQQPF924c1C5vpDwXcWo5FCEMzcHT195x’ is an empty token account in our wallet.

To check the balance of our token i.e. number of tokens that we have in our newly created account, run the following command.


![7](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/7_solana_check_balance.png)

The process of creating new tokens on the blockchain is known as “minting”. Let’s mint some new tokens!
To do so, we can use the following command.

```
spl-token mint <token address> <number of tokens to be minted>
```


![8](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/8_solana_token_mint.png)


To confirm that the newly created tokens have been added to your account, run the command for checking the balance of your account, as we had done earlier.

Congratulations, now you can mint infinite number of tokens for yourself and your friends! \( ﾟヮﾟ)/

## Limiting Total Supply and Burning our tokens

You might create a lot of tokens, distribute it with your friends, who might further distribute it to more of their friends - which we’ll see in a bit. Let us check how many tokens have I created and are currently being used by people on the blockchain. The circulating supply of a token refers to the total number of tokens that are being used by people for transactions. To view the circulating supply of your token, run the following command.

```
spl-token supply <token address>
```


![9](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/9_solana_check_supply.png)


We can create as many tokens as we want, there is no limit. That’s because we possess the “minting authority” for minting new tokens.
Let’s say you are creating tokens to raise money for your next project. You plan on creating 100 tokens and sell it to your investors that represents their ownership of the project. The investors might be sceptical to invest in your project as you possess the ability to always create more tokens and reduce their ownership in the project. Hence, they would want you to “renounce the ownership” of your token. That way, there’ll always be only 100 tokens in circulation forever.  
Solana provides us the ability to disable our minting authority, and never enable it back. We can do so by running the following command.

```
spl-token authorize <token address> mint –disable
```


![10](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/10_solana_authorize.png)


We have now renounced our ability to mint new tokens. If we do try to mint new tokens, we encounter an error.


![11](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/11_solana_mint_test.png)


Let’s say we want to “burn” our token, i.e. remove tokens that we own in our account out of circulation, so that they can never be used again. We can do so by running the following command.

```
spl-token burn <source token account address> <tokens to be burnt>
```


![12](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/12_solana_burn.png)


## Distributing with your friends

Let’s say you want to share your tokens with your friends. To send someone your token, they should be holding an SPL wallet themselves. A very popular option is the Phantom wallet. Phantom wallet offers us the ease of transacting on the Solana blockchain, through a chrome extension.
To add Phantom wallet to your browser, visit https://phantom.app/ and click on “Add to Chrome/Firefox”. Once the extension is installed, click on “Create a new wallet”. It’ll ask you to create a new password for your Phantom wallet extension and ask you to copy the “seed phrase”. Store this seed phrase somewhere safe and never share this seed phrase with anyone.
This seed phrase is a string that is used to give full access to sending and receiving tokens from your wallet. In case you change your browser or laptop, you can use this seed phrase to recover your original wallet. Anyone who has your seed phrase, can access your wallet and then perform transactions through it - so keep it safe!

Since in this quest we are transacting in devnet, we can change the network in Phantom to devnet. To do so, click on the cog wheel in the bottom right corner of your Phantom wallet, click on “Change network” and select “Devnet”.


![13](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/13_phantom_home.png) ![14](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/14_phantom_settings.png)


You can find out the wallet address of your Phantom wallet by clicking on the wallet’s name.

Your wallet address is your public key of the account created by you. This public key acts as your identity on the Solana Blockchain. And for verifying your identity, you could combine your public and private key.

In the above image, when you click on “Wallet 1” in the top bar, it’ll automatically copy the wallet’s public address. This public address can then be used to receive transactions. Let’s say, your friend’s wallet address is “FMVbLmfzoL9muizfhTPUxmm4Mwr4SxpxBFjEUqHHnhDy” and you wanted to send them some of your tokens. As we had mentioned earlier, for an SPL wallet to transact in a particular token, it needs to have an “account” for that token.

Your friend can add an account for your token in their wallet right in Phantom wallet by clicking on “Manage token list”.
Paste the token address over here of the token which you want to create an account for. You can give any token name and symbol you want for the new token.


![15](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/15_phantom_address_page.png) ![16](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/16_phantom_token_metadata.png)


Once the token account has been added to Phantom, we can now send the money to this wallet address. To send them our token, run the following command

```
spl-token transfer <your token account address> <total amount> <receiver’s wallet address>
```

We can verify the presence of our newly transferred token by checking Phantom wallet of your friend for a new token. It’ll be listed as an unknown token in the Phantom wallet’s homepage.


![17](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/17_phantom_token_balance.png)


In the above image, we can see the number of tokens that we hold (150) and the last 5 characters of our token address.

## Naming your Tokens

In Phantom wallet, we see that our token is listed as an “Unknown Token”. If we want our token to have a widely recognised name, symbol and image, we need to send a pull request to the [solana-labs/token-list: The community maintained Solana token registry repository](https://github.com/solana-labs/token-list).


![18](https://github.com/altsam/create_crypto_with_solana_cli/raw/main/learn_assets/18_github_image.png)

Add an entry to the “solana.tokenlist.json” file in the “src/tokens” directory.
The JSON entry would have the following structure.

```
{
   "chainId":101,
   "address":"your token address",
   "symbol":"your token symbol",
   "name":"Token Name",
   "decimals":"<number of decimals your token supports>",
   "logoURI":"the CDN link to your token's image",
   "tags":[
      "tags_if_any"
   ],
   "extensions":{

   }
}
```

Once the PR gets approved, you’ll be able to view the token image and name on every wallet in the Solana ecosystem.

## What’s next?

Now that you know how to create your very own cryptocurrency on Solana, in the upcoming quests we’ll see how to do it in Javascript and by writing our own Rust programs. Before you do that, don't forget to claim your NFT reward for succesfully completing this quest from [Layer3](https://alpha.layer3.xyz/task/create-your-personal-cryptocurrency-using-solana-cli)!
