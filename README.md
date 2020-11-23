


# Masternode Setup - Step by step guide
 

Requirements: 	
1.) VPS for example on vultr or AWS on Amazon Services or Digital Ocean (on digitalocean you can get bonus 50$ for 30 days)
2.) for 1 Masternode you need a wallet with 50001 APH Coins (1 coin for the fees)

Feel free to use our reflinks to signup: 
vultr:  <a href="https://www.vultr.com/?ref=7811287"><img src="https://www.vultr.com/media/banner_2.png" width="468" height="60"></a>

Feel free to use our reflinks to signup: 
DigitalOcean ( to get the Bonus of 50$ ) you can use this link: https://m.do.co/c/620c3ac29a40
 
## start in the wallet 
in wallet: Open Debug console: 

```bash
createmasternodekey
```

<table>
<tr><td>example</td></tr>
<tr><td>652FzuBw4v6ijn8fPw8843oh1NmSWBDpSLR1nipyCxkU73auGBx</td></tr>
</table>

```bash
getaccountaddress "MN1"  
```

<table>
<tr><td>example</td></tr>
<tr><td>GL75xQoKGrvgwdT5QaafVwxYihgvfdo7Xt</td></tr>
</table>

send exact 75000 Coins to the address (confirmation need: 15) 


# Installation: for Security use SSH on your vps!!

setup start with security on vps in putty (firewall)

```bash
sudo ufw allow 22
```
```bash
sudo ufw allow 80
```
```bash
sudo ufw allow 5662
```
```bash
sudo ufw enable
```
You will be prompted with "Yes or no". type y and press enter

```bash
sudo ufw default deny
```

start install the requirements on VPS:

```bash
sudo apt-get update
```
```bash
sudo apt-get upgrade -y
```
```bash
sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3 libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-test-dev libboost-thread-dev libboost-all-dev libboost-program-options-dev -y
```
```bash
sudo apt-get install libminiupnpc-dev libzmq3-dev libprotobuf-dev protobuf-compiler unzip software-properties-common -y
```
```bash
sudo add-apt-repository ppa:bitcoin/bitcoin
```
You will be prompted with "Enter". press enter

```bash
sudo apt-get update
```

download the wallet-client, tx and daemon file

```bash
sudo wget https://github.com/apholding/APH-Wallets/releases/download/v1042/APH-1042-Linux-Daemon.zip
```
fillout the password of your username and press enter


```bash
unzip APH-1042-Linux-Daemon.zip
```
```bash
sudo chmod +x apholdingd
```
```bash
sudo chmod +x apholding-tx
```
```bash
sudo chmod +x apholding-cli
```
```bash
sudo mv apholdingd apholding-cli apholding-tx /usr/bin/
```
```bash
sudo apt-get install libdb4.8-dev libdb4.8++-dev -y
```
```bash
mkdir $HOME/.apholding
```
```bash
nano $HOME/.apholding/apholding.conf
```

copy this with your details in th conf. file (choose only another good password, you need your masternode genkey from wallet and the ip address of the vps server)
```bash
#----
rpcuser=rpc_apholding
rpcpassword=chooseagoodpassword
rpcallowip=127.0.0.1
#----
listen=1
server=1
daemon=1
maxconnections=64
#----
masternode=1
masternodeprivkey=your-MASTERNODE-GENKEY-from-debugconsole
externalip=IP-address
addnode=178.254.12.25
addnode=178.254.28.153
addnode=178.254.29.39
#----
```
save this file by pressing CONTROL+O and press enter
close this file by pressing CONTROL+X

# start the vps server with

```bash
apholdingd
```
if everything is fine: you get an output: apholding server starting




### back in wallet
 
go to debug console

```bash
getmasternodeoutputs
```
<table>
<tr><td>example</td></tr>
 <tr><td>{</td></tr>
<tr><td>    "txhash": "c8ab8aa43d50cae6bf2b89b09f124bd83beaec00537884be8ec6585d1922", </td></tr>
<tr><td>     "outputidx": 1 {</td></tr>
<tr><td>   }</td></tr>
</table>


# Configure masternode.conf file (look at the example in file), reopen wallet and start masternode in debug console

<table>
<tr><td>example for masternode in masternode.conf file </td></tr>
<tr><td>mn1 IP_OF_THE_SERVER:14198 MASTERNODE_GENKEY TX_HASH TX_OUTPUTS</td></tr>
<tr><td>mn1 123.12.15.14:16364 652FzuBw4v6ijn8fPw8843oh1NmSWBDpSLR1nipyCxkU73auGBx c8ab8aa43d50cae6bf2b89b09f124bd83beaec00537884be8bae6585d1922 1</td></tr>
</table>

save file, reopen wallet and start in debug console !

```bash
startmasternode alias false MN1
```

