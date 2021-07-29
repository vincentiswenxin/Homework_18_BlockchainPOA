# Homework_18_BlockchainPOA

Hello Everyone,

Please use the following guide to setting up a Proof of Authority(PoA) consensys algorithm on the Ethereum testnet.
Follow this step by step instruction, you will master it in no time!

## Before you start, make sure you have the following software installed

1. **Git Bash https://gitforwindows.org/**

Git for Windows focuses on offering a lightweight, native set of tools that bring the full feature set of the Git SCM to Windows while providing appropriate user interfaces for experienced Git users and novices alike.

Git for Windows provides a BASH emulation used to run Git from the command line. *NIX users should feel right at home, as the BASH emulation behaves just like the "git" command in LINUX and UNIX environments.


2. **MyCrypto https://mycrypto.com/**

Download MyCrypto from https://download.mycrypto.com/ and follow the installation instructions.

3. **Go Ethereum Tool kit https://geth.ethereum.org/**

Go Ethereum is one of the three original implementations (along with C++ and Python) of the Ethereum protocol. It is written in Go, fully open source and licensed under the GNU LGPL v3.

Please refer to https://geth.ethereum.org/downloads/ scroll down to stable release and download Geth & Tools.

## Let's build our own blockchain

**Step 1: Open Gitbash in the folder where you downloaded the Go Ethereum Tools.**

**Step 2: Generating 2 nodes**

In Gitbash to generate Node1 & Node2:
input:
* `./geth --datadir node1 account new`
* `./geth --datadir node2 account new`
1. set a password, enter and repeat password.
2. one public address key & a secret file key will be given for each Node. **Save the keys for later**.

    ![node](/Screenshots/Node.png)

**Step 3: Building and Configuring the Genesis block**
In Gitbash input: `./puppeth`
1. name your network, my choice is `vincent`

2. select the option to `configure a new genesis block`

3. Choose the `Clique (Proof of Authority)` consensus algorithm.

4. Paste both account addresses from the first step one at a time into the list of accounts to seal.

**If your insert does not work, try `shift + insert`**

5. Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

6. You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

    ![genesis_config](/Screenshots/Genesis_Block_config.png)

7. for choice of seconds each block takes, you can just hit enter for default or you can enter you own time setting, and when you are back at the main menu, choose the `"Manage existing genesis"` option.

8. Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.

    ![manage_and_export](/Screenshots/manage_and_export.PNG)

**Step 4: Initialize nodes and start mining**
1. In Gitbash input: following commands to initialize node 1 & 2.
**change `yournetworkname` to your own network name, for example, my network name is vincent**
`./geth --datadir node1 init yournetworkname.json`
`./geth --datadir node2 init yournetworkname.json`

    ![Initial_node](/Screenshots/Initial_node.PNG)

2. In Gitbash input: the following command for node 1.
**change `Your Node 1 Public Address Here` to your own public address**

    `./geth --datadir node1 --unlock "Your Node 1 Public Address Here" --mine --rpc --syncmode "full" --snapshot=false --allow-insecure-unlock`

* Type your password and hit enter - even if you can't see it visually!

    Node1:
    ![node1](/Screenshots/node1.PNG)

3. open a **new Gitbash/terminal** and change directories to Go Ethereum Tools.

4. In Gitbash input: the following command for node 2.
    `./geth --datadir node2 --unlock "Your Node 2 Public Address Here" --mine --port 30304 --bootnodes "enode://of your Node 1" --ipcdisable --allow-insecure-unlock1`

    **NOTE: you need to use your own Node 2 Public Address and enode address from node 1, you can find the enode in the returned value in node 1 activation terminal**
* Type your password and hit enter - even if you can't see it visually!

    Node2:
    ![node2](/Screenshots/node2.PNG)


**Step 5: start using you testnet**

1. Open the MyCrypto app, then click Change Network at the bottom left

2. Click "Add Custom Node", then add the custom network information that you set in the genesis.

3. Make sure that you scroll down to choose Custom in the "Network" column.

4. Type `ETH` in the Currency box

5. In the Chain ID box, type the chain id you generated during genesis creation. my is `333`

6. In the URL box type:` http://127.0.0.1:8545.` This points to the default RPC port on your local machine.

7. Finally, click Save & Use Custom Node.

    ![mycrypto_setup](/Screenshots/mycrypto_setup.PNG)


**Step 7: Testing**
1. After changing your network to the custom one that was just created.
2. select the `View & Send` tab on the left 
3. at the bottom of the screen select the `Keystore File`.
4. click on `Select Wallet File` and navigate to the to your Node 1 directory and then select the UTC file
5. provide your password when prompted and then click `Unlock`
6. In the To Address box, type the account address from Node2, then fill in an arbitrary amount of ETH
7. Confirm the transaction by clicking `Send Transaction`, and the `Send` button in the pop-up window.
8. Click the `Check TX Status` when the green message pops up and confirm the logout
9. You should see the transaction go from `Pending` to `Successful` in around the same blocktime you set in the genesis.
10. You can click the `Check TX Status` button to update the status.
    ![transactions](/Screenshots/transactions.PNG)

**Good Luck on Your Own Testnet!**