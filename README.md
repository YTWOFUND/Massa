# Massa
### Massa node Installation Instructions.

[Official documentation](https://docs.massa.net/en/latest/testnet/install.html)

System requirements:</br>
CPU: 4 Core</br>
RAM: 8 Gb</br>
SSD: 100 Gb</br>
OS: Ubuntu 20.04 LTS</br>

### Installing the Massa Node

1. Preparing the server.
```
sudo apt update && sudo apt-get install libclang-dev
```
2. Downloading binary files.
```
wget https://github.com/massalabs/massa/releases/download/TEST.20.0/massa_TEST.20.0_release_linux.tar.gz
```
3. Unpack the downloaded archive
```
tar zxvf massa_TEST.20.0_release_linux.tar.gz
```
4. Before starting the node, we will write the server ip-address in the config.
```
sudo tee <<EOF >/dev/null $HOME/massa/massa-node/config/config.toml
[network]
routable_ip = "`wget -qO- eth0.me`"
EOF
```
5. Launching the node.
```
cd $HOME/massa/massa-node/ && ./massa-node
```
6. Stop node Ctrl+C

7. Create a service file. (change password to your own)
```
printf "[Unit]
Description=Massa Node
After=network-online.target
[Service]
User=$USER
WorkingDirectory=$HOME/massa/massa-node
ExecStart=$HOME/massa/massa-node/massa-node -p <password>
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target" > /etc/systemd/system/massad.service
```
8. Launch the node.
```
sudo systemctl daemon-reload && sudo systemctl enable massad && sudo systemctl restart massad
```
9. Checking the logs.
```
sudo journalctl -f -n 100 -u massad
```

WE WAITING FOR THE NODE FOR BOOTSRAPE

10. Launching the client.
```
cd $HOME/massa/massa-client/ && ./massa-client
```
11. Generating a new wallet.
```
wallet_generate_secret_key
```
12.See address.
```
wallet_info
```
13. Request test tokens in [project discord](https://discord.com/channels/828270821042159636/866190913030193172).

14. Enable staking.
```
node_start_staking <wallet address> 
```
15. Buying a roll.
```
buy_rolls <wallet address> 1 0
```
16. Checking the purchase of a roll.
```
wallet_info
```
17. We send our IP to Discord Massa Bot, in the terminal we enter the following command.
```
node_testnet_rewards_program_ownership_proof <wallet address> <id from Discord>
```
18. We send the result of the received command to Massa Bot in Discord.

19. We track the accrual of points from Massa Bot with the "info" command.
