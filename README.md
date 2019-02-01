SETUP A MASTERNODE 

Go to “Tools”. 
Click “Debug console”. 
This is the console where you will execute all commands.

Create a masternode private key.

masternode genkey

Example output

6eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo

Show your collateral address.

getaccountaddress "MN1"

Example output

Nad4xtgdwf7c5y45ruy5MWtVY43zYMCvva

Keep note of the masternode private key and the collateral address.


Setup the VPS
Install Ubuntu Server 16.04 on a VPS.

Update your Ubuntu machine.

sudo apt-get update
sudo apt-get upgrade

Install the required dependencies.

sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3 libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-test-dev libboost-thread-dev libboost-all-dev libboost-program-options-dev
sudo apt-get install libminiupnpc-dev libzmq3-dev libprotobuf-dev protobuf-compiler unzip software-properties-common

Install Berkeley DB.

sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev


wget "https://github.com/1apdeveloper/mn-pos-Coin-APHolding/blob/master/apholdingd" 
wget "https://github.com/1apdeveloper/mn-pos-Coin-APHolding/blob/master/apholding-cli" 
wget "https://github.com/1apdeveloper/mn-pos-Coin-APHolding/blob/master/apholding-tx" 
wget "https://github.com/1apdeveloper/mn-pos-Coin-APHolding/blob/master/apholding-qt" 


Install the daemon and tools.

sudo mv apholdingd apholding-cli apholding-tx /usr/bin/

Create the config file.

mkdir $HOME/.apholding
nano $HOME/.apholding/apholding.conf

Paste the following lines in apholding.conf.

#----
rpcuser=rpc_apholding
rpcpassword=YOUR_FREE_PASSWORD_CHOOSE_A_GOOD_ONE
rpcallowip=127.0.0.1
#----
listen=1
server=1
daemon=1
maxconnections=64
#----
masternode=1
masternodeprivkey=REPLACE_WITH_MASTERNODE_PRIVATE_KEY
externalip=REPLACE_WITH_EXTERNAL_IP_OF_VPS
#----

Replace the text “REPLACE_WITH_MASTERNODE_PRIVATE_KEY” with the “masternode private key” that you created using the command “masternode genkey”. 

E.G. masternodeprivkey=75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo

Replace the text “REPLACE_WITH_EXTERNAL_IP_OF_VPS” with the external IP address of your VPS. 

E.G. externalip=136.144.171.201

Start your node with the following command.

apholdingd

Setup the control wallet (2/2)
Transfer the required amount of coins to the “collateral address” that you created using the command “getaccountaddress "MN1"”.

Wait until the transaction has the required masternode confirmations.

Go to Tools. 
Click Debug console.

Enter the following command.

masternode outputs

Example output


[
  {
    "txhash": "4529a5caf40178d6911ab71e61d6952a6cec8710405d8dc912d8e8a760a2ba24c",
    "outputidx": 1
  }
]


Go to “Tools”. 
Click “Open Masternode Configuration File”.

Modify the following line and paste it into notepad.

MN1 123.111.222.201:9999 6eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo 4529a5caf40178d6911ab71e61d6952a6cec8710405d8dc912d8e8a760a2ba24c 1

MN1 - Alias for your masternode.

136.144.171.201 - External IP of your VPS.

9999 - Replace with P2P port of your coin.

75eqvNfaEfkd3YTwQ3hMwyxL2BgNSrqHDgWc6jbUh4Gdtnro2Wo - Masternode private key from the command “masternode genkey”.

429a5caf40178d6911ab71e61d6952a6cec8710405d8dc912d8e8a760a2ba24c - Value “txhash” from the command “masternode outputs”.

1 - Value “outputidx” from the command “masternode outputs”.

Save the file and close notepad.

Shutdown your wallet and re-open your wallet.

Go to “Settings”. 
Click “Unlock Wallet”.

Enter your wallet passphrase and unlock your wallet.

Go to “Tools”. 
Click “Debug console”.

Start your masternode using the command.

startmasternode alias false MN1

It will take +/- 30 minutes to activate your masternode.
