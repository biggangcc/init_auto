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

## Step 4: 查看日志

```
journalctl -u initia-node -f -o cat
```
To exit the logs, type Ctrl+C.

## Step 5: 创建 Initia钱包

```
ansible-playbook create_initia_wallet.yml
```
Once completed, you will obtain the address of the Initia wallet. Save it for requesting testnet funds and further operations.

## Step 6: 领取水龙头代币

领取教程参看我的YT


## Step 7: 检查节点同步到最新，必须要等几个小时才能同步到最新，只有同步到最新时，才继续下面的操作、

```
initiad status | jq
```


## Step 8: 注册验证器
使用你的钱包地址进行注册

```
ansible-playbook register_initia_node.yml
```
During this step, you will be prompted to input the following information:

Moniker: "node_name"
Details: "a phrase of your choice"
Website: "your website"

## Step 9: 查看验证器状态

```
initiad query mstaking validator <你的验证器地址>
```

## Step 10: 设置Oracle

```
ansible-playbook setup_oracle.yml
```

## 额外的命令
停止服务
To stop the Initia node:
```
sudo systemctl stop initia-node
```

开启服务
To start the Initia node:
```
sudo systemctl start initia-node
```

移除节点
```
ansible-playbook remove_node_initia.yml
```










