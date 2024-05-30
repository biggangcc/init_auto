# Initia Node Deployment

为了让大家更方便的进行节点的部署，特意写了这个安装器。

大家按照


## Prerequisites

这是官方推荐配置：

Recommended:

操作系统: Linux Ubuntu 22.04
CPU: 4-core
RAM: 16GB
硬盘存储: 1TB SSD

VPS购买：
https://aeza.net/?ref=436742


使用方法：

## Step 1: 安装系统依赖


```
sudo apt update && sudo apt upgrade -y
sudo apt install git ansible -y

```
确保你的Ansible版本号是 2.15 或以后的版本:

```
ansible --version

```
## Step 2: 克隆安装器

```
https://github.com/BigGangCrypro/initia_node.git
cd initia_node
```

## Step 3: 安装Initia Node
在安装过程中，会提示你输入节点名称和快照的节点高度

节点名称自己起个名字就好

快照节点高度根据：https://polkachu.com/testnets/initia/snapshots  这个来找到最新的高度快照，然后输入。

```
ansible-playbook install_initia_node.yml

```
Example of input prompts:

```
Enter the node name: mynode
Enter the block height of the polkachu snapshot: 1234567
```

## Step 4: Viewing Node Logs
To view the logs for the Initia node:

```
journalctl -u initia-node -f -o cat
```
To exit the logs, type Ctrl+C.

## Step 5: Creating an Initia Wallet
After installing the node, create an Initia wallet essential for network operations:

```
ansible-playbook create_initia_wallet.yml
```
Once completed, you will obtain the address of the Initia wallet. Save it for requesting testnet funds and further operations.

## Step 6: Requesting Initia Testnet Funds
To request testing funds on the Initia network, check the #faucet-verification channel on the Initia Discord. Then, go to the Initia faucet website and claim test tokens by typing your wallet number.

Note: Due to high demand, you may need to wait 20 minutes for the tap role to be checked. You can only claim 30 INIT once every 24 hours.

## Step 7: Checking Node Synchronization
To ensure your node is fully synchronized with the Initia blockchain:

```
initiad status | jq
```

Synchronization takes several hours. Once the catching_up variable is false, your node is fully synchronized and ready for further operations.

## Step 8: Registering the Initia Node as a Validator
Finalize your node configuration by registering your node as a validator and linking it to your Initia wallet. Ensure your node is synchronized with the blockchain and you hold Initia tokens in your wallet. Then, run this command:


```
ansible-playbook register_initia_node.yml
```
During this step, you will be prompted to input the following information:

Moniker: "node_name"
Details: "a phrase of your choice"
Website: "your website"

## Step 9: Viewing Validator State
You can check the status of your validator by executing:

```
initiad query mstaking validator <validator_address>
```
Replace <validator_address> with your validator's wallet address provided at the end of the playbook execution.

## Step 10: Setting Up the Oracle
To set up the Oracle for Initia, execute the following playbook:

```
ansible-playbook setup_oracle.yml
```
This will configure and run the Oracle sidecar, enabling essential components for the Oracle and Market functionalities.

## Additional Information
Stopping the Service
To stop the Initia node:
```
sudo systemctl stop initia-node
```

Starting the Service
To start the Initia node:
```
sudo systemctl start initia-node
```

Removing the Initia Node
To remove the Initia node, run the playbook for removal:
```
ansible-playbook remove_node_initia.yml
```
Ensure to back up any important data before removing the node, as this action may delete node data.

Conclusion
That's it! You have successfully deployed an Initia node, thus contributing to the robustness of the network and earning potential rewards. Join the Initia community on Discord and Twitter to stay informed about the project.

Thank you for taking the time to read this guide. If you have any questions or would like to continue the conversation, feel free to join the Initia community on Discord.

Stay updated and connected: Follow us on Twitter, join our Telegram group, Discord server, and subscribe to our YouTube channel.









