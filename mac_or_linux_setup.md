Note: This guide comes courtesy of [Buildspace](https://buildspace.so). Do check them out if you get the chance.

## 🍎 Setting up Solana on an Intel macOS or Linux Machine.

This guide will get you up and running with the Solana enviroment on your local machine. We made modifications that will get you to becoming a Solana Master faster with less headaches 🙂.

Let's kick it off!

### ⚙️ Install Rust.

In Solana, programs are written in Rust! If you don't know Rust don't worry. As long as you know some other language — you'll pick it up over the course of this project.

To install Rust we will open up our terminal and run this command:

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

You will be prompted with multiple options to install. We are going to go with default entering 1 and then enter!

Once you're done, go ahead and restart your terminal and then verfiy it was installed by entering:

```bash
rustup --version
```

Then, make sure the rust compiler is installed:

```bash
rustc --version
```

Last, let's make sure Cargo is working as well. Cargo is the rust package manager.

```bash
cargo --version
```

As long as all those commands output a version and didn't error, you're good to go!

### 🔥 Install Solana - THIS IS WHAT WE CAME FOR!

We are to download with this command:

```bash
sh -c "$(curl -sSfL https://release.solana.com/v1.9.5/install)"
```

This might take some time, so don't be alarmed! >nce you install Solana, it may output a message like "Please update your PATH environment variable" and it'll give you a line to copy and run. Go ahead and copy + run that command so your PATH gets setup properly, then run this to make sure everything is in working order:

```bash
solana --version
```

Next thing you'll want to do is run these three commands separately:

```bash
solana config set --url localhost
solana config get
```

This will output something like this:

```bash
Config File: /Users/nicholas-g/.config/solana/cli/config.yml
RPC URL: http://localhost:8899
WebSocket URL: ws://localhost:8900/ (computed)
Keypair Path: /Users/nicholas-g/.config/solana/id.json
Commitment: confirmed
```

This means that Solana is set up to talk to our local network! When developing programs, we're going to be working w/ our local Solana network so we can quickly test stuff on our computer.
The last thing to test is we want to make sure we can get a local Solana node running. Basically, remember how we said that the Solana chain is run by "validators"? Well — we can actually set up a validator on our computer to test our programs with:

```bash
solana-test-validator
```

This may take a bit to get started but once it's going you should see something like this:

![Untitled](https://i.imgur.com/FUjRage.jpg)

Boom!! You're now running a local validator. Pretty cool :).

### ☕️ Install Node, NPM, and Mocha

Pretty solid chance you already have Node and NPM. When I do node --version I get v16.0.0. The minimum version is v11.0.0. If you don't have node and NPM, get it [here](https://nodejs.org/en/download/).

After that, be sure to install this thing called Mocha. It's a nice little testing framework to help us test our Solana programs.

```bash
npm install -g mocha
```

### ⚓️ The magic of Anchor

We're going to be using this tool called "Anchor" a lot. **Basically, it makes it really easy for us to run Solana programs locally and deploy them to the actual Solana chain when we're ready!**

Anchor is a *really early projec*t run by a few core devs. You're bound to run into a few issues. Be sure to join the [Anchor Discord](https://discord.gg/8HwmBtt2ss) and feel free to ask questions or [create an issue](https://github.com/project-serum/anchor/issues) on their Github as you run into issues. The devs are awesome. 

**BTW — don't just join their Discord and ask random questions expecting people to help. Try hard yourself to search through their Discord to see if anyone else has had the same question you have. Give as much info about your questions as possible. Make people want to help you lol.**

_Seriously — join that Discord, the devs are really helpful._

Note: If you're on Linux, there are some special instructions you can follow [here](https://project-serum.github.io/anchor/getting-started/installation.html#install-anchor). 

To install Anchor, go ahead and run:

```bash
cargo install --git https://github.com/project-serum/anchor anchor-cli --locked
```

The above command may take a while and your computer may get a little toasty 🔥. Once it's done, it may ask you to update you path, remember to do that.

From here run:

```bash
anchor --version
```

If you got that working, nice, you have Anchor!!

We'll also use Anchor's npm module and Solana Web3 JS — these both will help us connect our web app to our Solana program!

```bash
npm install @project-serum/anchor @solana/web3.js
```

### 🏃‍♂️ Create a test project and run it.

Okay, we're _nearly done_ haha. The last thing we need to do to finalize installation is to actually run a Solana program
locally and make sure it actually works.

Before we begin, make sure you have `yarn` installed on your machine:

```bash
brew install yarn
```

We can make the boilerplate Solana project named `myepicproject` with one easy command:

```bash
anchor init myepicproject --javascript
cd myepicproject
```

`anchor init` will create a bunch of files/folders for us. It's sort of like `create-react-app` in a way. We'll check out all the stuff it's created in moment.

### 🔑 Create a local keypair.

Next thing we need to do is actually generate a local Solana wallet to work with. Don't worry about creating a passphrase for now, just tap "Enter" when it asks.

```bash
solana-keygen new 
```

What this will do is create a local Solana keypair — which is sorta like our local wallet we'll use to talk to our programs via the command line. If you run solana config get you'll see something called Keypair Path. That's where the wallet has been created, feel free to check it out :).
If you run:

```bash
solana address 
```

You'll see the public address of your local wallet we just created.

### 🥳 Let's run our program.

When we did ```anchor init``` it created a basic Solana program for us. What we want to do now is:
1. Compile our program.
2. Spin up solana-test-validator and deploy the program to our local Solana network w/ our wallet. This is kinda like deploying our local server w/ new code.
3. Actually call functions on our deployed program. This is kinda like hitting a specific route on our server to test that it's working.

Anchor is awesome. It lets us do this all in one step by running:

```
anchor test
```

This may take a while the first time you run it! As long as you get the green words at the bottom that say "1 passing" you're good to go!!

**Note: If you receive the message node: --dns-result-order= is not allowed in NODE_OPTIONS this mean you are on an older version of Node and technically, this didn't pass! Since I tested this all with Node v16.13.0 I would highly suggest you just upgrade to this version. Upgrading node is a pain, learn more here. I like using nvm.**

**Congrats you've successfully set up your Solana environment :).** It's been quite the journey, but, we made it fam.
