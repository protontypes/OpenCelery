<img align="middle" src="./docs/OpenSelery-04.png" width="400"> 

### Automated Contribution Financing 

> OpenSelery is a decentralized framework for funding distribution in free software development. It offers transparent and adaptable funding of contributors on Github hosted project and it's dependencies integrated into Github Action.

[![](https://img.shields.io/gitter/room/protontypes/openselery)](https://gitter.im/protontypes/openselery)        
[![Actions Status](https://github.com/protontypes/openselery/workflows/openselery/badge.svg)](https://github.com/protontypes/openselery/actions?query=workflow%3Aopenselery)![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/protontypes/openselery?logo=docker)         

[![stability-experimental](https://img.shields.io/badge/stability-experimental-orange.svg)](https://github.com/emersion/stability-badges#experimental)   
![Balance](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/protontypes/openselery/openselery/balance_badge.json&style=flat&logo=bitcoin)![Balance](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/wiki/protontypes/openselery/openselery/native_balance_badge.json&style=flat&logo=bitcoin)         
[![Donate with bitcoin](https://badgen.net/badge/Donate/3PVdiyLPR7MgaeFRJLW9mfuESZS2aAPX9w/orange?icon=bitcoin)](https://raw.githubusercontent.com/wiki/protontypes/openselery/openselery/wallet_qrcode.png)
[![Transaction History](https://badgen.net/badge/icon/Transaction%20History?icon=bitcoin&label)](https://github.com/protontypes/openselery/wiki/Transaction-History)

*OpenSelery is in an experimental state. The amount of funding on your wallet should therefore be limited.*



## Features

* Transparent payout of Github project contributors with detailed [transaction history](https://github.com/protontypes/openselery/wiki/Transaction-History)
* User defined payout configuration by the [selery.yml](https://github.com/protontypes/openselery/blob/master/selery.yml).
* Dependency scanning for most languages to even include developers of your dependencies.
* Distribution of money is done via Coinbase. Further payment methods like Paypal or Uphold will soon been supported. 
* Investors can see a transparent payout logs in the [public action logs](https://github.com/protontypes/openselery/actions?query=workflow%3Aopenselery).
* Self generated [QR code](https://raw.githubusercontent.com/wiki/protontypes/openselery/openselery/wallet_qrcode.png) for secure investment into your project. Wallet address is been double checked against the configured Coinbase wallet.
* Minimal adaptations of your Github project shown in the [seleryexample](https://github.com/protontypes/seleryexample).
* Automated user information about deposited funding send to the Github user email address with a thank you note.
* Simple simulation on your project to investigate distribution on past git history. 



## How it works

1. OpenSelery is configured based on the selery.yml file and runs completely decentralized as a Github Action.

2. Triggers with every push on the master branch.

3. Gathers contributor information about the target project via the Github and Libraries.io API.

4. Filters out contributors that not made the email address visible in the Github profile.

5. Creates user defined funding distribution weights based on different projects contribution assessment: Minimum Contribution, Activity, Solved Issues, ...

6. Sums the weights together to the combined weights. 

7. Splits the funding between contributers based on different modes. 

8. Pays out Cryptocurrency to the chosen contributor email addresses via the Coinbase API. Contributors without a Coinbase account will get a email to claim the donation.

   

## Demo

[![asciicast](https://asciinema.org/a/353518.svg)](https://asciinema.org/a/353518)



## Continuous Integration  

Use the [Template](https://github.com/protontypes/seleryexample) to integrate OpenSelery into any Github project. 



## Command Line Usage 

1. Install [docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/):

```bash
cd ~
git clone https://github.com/protontypes/openselery.git
cd openselery
./build.sh
```

2. Create a dedicated Coinbase account with limited amounts. OpenSelery needs of API tokens from [Github](https://github.com/settings/tokens) and [Libraries.io](https://libraries.io/api) in simulation mode.

3. Copy a [selery.yml](https://github.com/protontypes/seleryexample) into your <target_project>. Set 'simulation: False' in your selery.yml 

4. Adjust and test different configuration in simulation mode on your project.

5. Buy some cryptocurrency. See the [price list](https://help.coinbase.com/en/coinbase/trading-and-funding/pricing-and-fees/fees.html) for transferring money into the coinbase account.

Configure the [access control settings](https://github.com/protontypes/openselery/wiki/Coinbase-Settings) of the automated Coinbase wallet.  

6. Never transfer or store large values with automated cryptocurrency wallets. Use [recurring automated buys](https://blog.coinbase.com/easier-recurring-buys-and-sells-on-coinbase-9a3cd7ea934e) to recharge you wallet on a regular base to avoid financial and security risks. Coinbase does not charge for transferring cryptocurrency from one Coinbase wallet to another

7. Create a read only token file for your user, where you store API keys and secrets:

```bash
mkdir ~/.openselery/
touch ~/.openselery/tokens.env
chmod 400 ~/.openselery/tokens.env
```

7. Add your API keys and secrets to the newly created file (`~/.openselery/tokens.env`). **Never store these tokens in a repository**.

```bash
COINBASE_TOKEN=XXXXXXXXXXXXXXXX
COINBASE_SECRET=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
GITHUB_TOKEN=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
LIBRARIES_API_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

8. Send cryptocurrency to weighted random product contributors with a valid visible email address on GitHub:

```bash
env $(cat ~/.openselery/tokens.env | xargs) ./run.sh ~/openselery
```

#### Run nativly on Debian / Ubuntu

1. Install Dependencies

```bash
sudo apt update && apt install git ruby ruby-dev ruby-bundler build-essentail curl python3-pip
cd openselery
bundle install 
python3 setup.py install 
```

2. Run OpenSelery

```bash
TARGET_DIR=<target_repository> && env $(cat ~/.openselery/tokens.env) python3 selery.py --config $TARGET_DIR/selery.yml --directory $TARGET_DIR --result results
```



## API Integration

OpenSelery is going to supports multiple APIs and assets in the near future:
- [x] Github 
- [x] Libraries.io
- [ ] Gitlab 
- [x] Coinbase
- [ ] Paypal (Already tested but requires a business account activation)
- [ ] Uphold



## Contribution

Contributors on the master branch will get emails with cryptocurrency from Coinbase. Only git profiles with emails on the Github profile page are considered.
Find out more in the [Contribution Guide](https://github.com/protontypes/openselery/wiki/Contribution-Guide).



<p align="center">
  <img src="docs/selery_workflow.png" width="500">
</p>



*Artwork by Miriam Winter and [undraw](https://undraw.co/)*