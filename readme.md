# ディレクトリ作成・Node.jsプロジェクトとして初期化
<!-- <img src="home.png"> -->


> 参考資料:https://zenn.dev/cauchye/articles/ethereum-contract-helloworld-local

# Node.jsプロジェクトを作成

> 参考資料:https://zenn.dev/cauchye/articles/ethereum-contract-helloworld-local  

```bash
# package.jsonを生成
npm init
# node_modulesとpackage-lock.jsonを生成
npm install  express --save
```

```bash
# expressパッケージをインストール
npm install  express --save
```

- "/"ディレクトリにindex.jsファイルを作成する  
> 以下を記述（テスト用）  
```js
//モジュールのインポート
const http = require('http');
const express = require('express');

//expressオブジェクトの生成
const app = express();

//getでリクエスト時に処理するコールバック関数指定
app.get("/", function(req, res){
    return res.send("Hello World");
});

//サーバの設定
const server = http.createServer(app);
server.listen(3000);
```

- node.jsの実行

```bash
# node.jsの実行
node index.js
```
> 以下にアクセス  
> http://localhost:3000/   

- Node.jsプロジェクトを作成は終わり

```bash
# フォルダを作成
mkdir contracts
# ディレクトリ移動
cd contracts
# package.jsonを生成
npm init -y
```

# hardhatでコントラクト開発環境を構築

> コントラクトのサンプルと、それをローカル開発用ネットワークへデプロイしたりテストするために必要なリソースが一気に作成されます。必要なパッケージ等もインストールされます。  

```bash
# hardhatパッケージをインストール
npx hardhat init
# 結果
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

👷 Welcome to Hardhat v2.6.4 👷‍

✔ What do you want to do? · Create a basic sample project
✔ Hardhat project root: · /Users/Masa/Desktop/test/contracts
✔ Do you want to add a .gitignore? (Y/n) · y
✔ Do you want to install this sample project's dependencies with npm (hardhat @nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers)? (Y/n) · y
```


# コントラクトをコンパイルしてバイトコードを生成
```bash
# contracts/artifacts/contracts/Greeter.sol/Greeter.jsonというファイルが生成
npx hardhat compile
```

# コントラクトの単体テスト

```bash
# 自動テストが実行
npx hardhat test
# 結果
  Greeter
Deploying a Greeter with greeting: Hello, world!
Changing greeting from 'Hello, world!' to 'Hola, mundo!'
    ✓ Should return the new greeting once it's changed (464ms)


  1 passing (465ms)
```


# ローカル開発用ネットワークを明示的に指定してコントラクトをテスト

```bash
# ローカル開発用ブロックチェーンネットワーク上で開発用のETHの残高があるアカウントのアドレスと秘密鍵の情報が一覧で表示された後、待機状態になります。
npx hardhat node
# 結果
Started HTTP and WebSocket JSON-RPC server at http://127.0.0.1:8545/

Accounts
========
Account #0: 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 (10000 ETH)
Private Key: 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80

Account #1: 0x70997970c51812dc3a010c7d01b50e0d17dc79c8 (10000 ETH)
Private Key: 0x59c6995e998f97a5a0044966f0945389dc9e86dae88c7a8412f4603b6b78690d

Account #2: 0x3c44cdddb6a900fa2b585dd299e03d12fa4293bc (10000 ETH)
Private Key: 0x5de4111afa1a4b94908f83103eb1f1706367c2e68ca870fc3fb9a804cdab365a

Account #3: 0x90f79bf6eb2c4f870365e785982e1f101e93b906 (10000 ETH)
Private Key: 0x7c852118294e51e653712a81e05800f419141751be58f605c371e15141b007a6

Account #4: 0x15d34aaf54267db7d7c367839aaf71a00a2c6a65 (10000 ETH)
Private Key: 0x47e179ec197488593b187f80a00eb0da91f1b9d0b13f8733639f19c30a34926a

Account #5: 0x9965507d1a55bcc2695c58ba16fb37d819b0a4dc (10000 ETH)
Private Key: 0x8b3a350cf5c34c9194ca85829a2df0ec3153be0318b5e2d3348e872092edffba

Account #6: 0x976ea74026e726554db657fa54763abd0c3a0aa9 (10000 ETH)
Private Key: 0x92db14e403b83dfe3df233f83dfa3a0d7096f21ca9b0d6d6b8d88b2b4ec1564e

Account #7: 0x14dc79964da2c08b23698b3d3cc7ca32193d9955 (10000 ETH)
Private Key: 0x4bbbf85ce3377467afe5d46f804f221813b2bb87f24d81f60f1fcdbf7cbf4356

Account #8: 0x23618e81e3f5cdf7f54c3d65f7fbc0abf5b21e8f (10000 ETH)
Private Key: 0xdbda1821b80551c9d65939329250298aa3472ba22feea921c0cf5d620ea67b97

Account #9: 0xa0ee7a142d267c1f36714e4a8f75612f20a79720 (10000 ETH)
Private Key: 0x2a871d0798f97d79848a013d4936a73bf4cc922c825d33c1cf7073dff6d409c6

Account #10: 0xbcd4042de499d14e55001ccbb24a551f3b954096 (10000 ETH)
Private Key: 0xf214f2b2cd398c806f84e317254e0f0b801d0643303237d97a22a48e01628897

Account #11: 0x71be63f3384f5fb98995898a86b02fb2426c5788 (10000 ETH)
Private Key: 0x701b615bbdfb9de65240bc28bd21bbc0d996645a3dd57e7b12bc2bdf6f192c82

Account #12: 0xfabb0ac9d68b0b445fb7357272ff202c5651694a (10000 ETH)
Private Key: 0xa267530f49f8280200edf313ee7af6b827f2a8bce2897751d06a843f644967b1

Account #13: 0x1cbd3b2770909d4e10f157cabc84c7264073c9ec (10000 ETH)
Private Key: 0x47c99abed3324a2707c28affff1267e45918ec8c3f20b8aa892e8b065d2942dd

Account #14: 0xdf3e18d64bc6a983f673ab319ccae4f1a57c7097 (10000 ETH)
Private Key: 0xc526ee95bf44d8fc405a158bb884d9d1238d99f0612e9f33d006bb0789009aaa

Account #15: 0xcd3b766ccdd6ae721141f452c550ca635964ce71 (10000 ETH)
Private Key: 0x8166f546bab6da521a8369cab06c5d2b9e46670292d85c875ee9ec20e84ffb61

Account #16: 0x2546bcd3c84621e976d8185a91a922ae77ecec30 (10000 ETH)
Private Key: 0xea6c44ac03bff858b476bba40716402b03e41b8e97e276d1baec7c37d42484a0

Account #17: 0xbda5747bfd65f08deb54cb465eb87d40e51b197e (10000 ETH)
Private Key: 0x689af8efa8c651a91ad287602527f3af2fe9f6501a7ac4b061667b5a93e037fd

Account #18: 0xdd2fd4581271e230360230f9337d5c0430bf44c0 (10000 ETH)
Private Key: 0xde9be858da4a475276426320d5e9262ecfc3ba460bfac56360bfa6c4c28b4ee0

Account #19: 0x8626f6940e2eb28930efb4cef49b2d1f2c9c1199 (10000 ETH)
Private Key: 0xdf57089febbacf7ba0bc227dafbffa9fc08a93fdc68e1e42411a14efcf23656e
```

- 次に、別のターミナルを立ち上げて、npx hardhat test --network localhostコマンドを実行する

```bash
# コントラクトのデプロイや、コントラクト内の関数の呼び出し等のログが出力
npx hardhat test --network localhost
# 結果
  Greeter
    ✓ Should return the new greeting once it's changed (305ms)


  1 passing (306ms)
```

- vscodeターミナルに戻ってみると表示が追加されている

```bash
# ...省略
web3_clientVersion (2)
eth_chainId
eth_accounts
eth_blockNumber
eth_chainId (2)
eth_estimateGas
eth_getBlockByNumber
eth_feeHistory
eth_sendTransaction
  Contract deployment: Greeter
  Contract address:    0x5fbdb2315678afecb367f032d93f642f64180aa3
  Transaction:         0x56edad30f88035fca33d621cfa061dac5a78487e71b4e68e3c80c974441b5d93
  From:                0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
  Value:               0 ETH
  Gas used:            497002 of 497002
  Block #1:            0x9cfc474d3ba7d1997257d8950fc370637b3aa39dad51c484c49fb1210743a788

  console.log:
    Deploying a Greeter with greeting: Hello, world!

eth_chainId
eth_getTransactionByHash
eth_chainId
eth_getTransactionReceipt
eth_chainId
eth_call
  Contract call:       Greeter#greet
  From:                0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
  To:                  0x5fbdb2315678afecb367f032d93f642f64180aa3

eth_chainId
eth_estimateGas
eth_feeHistory
eth_sendTransaction
  Contract call:       Greeter#setGreeting
  Transaction:         0x94ec084ff3de7b6619e1f4a618181bbc8e882f7b61cf881c6f15b43f25ad0d49
  From:                0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
  To:                  0x5fbdb2315678afecb367f032d93f642f64180aa3
  Value:               0 ETH
  Gas used:            35426 of 35702
  Block #2:            0xd142ebd191620cef185fbd6ffe791ef4205d16a7c8830966b53bb7b9959dd906

  console.log:
    Changing greeting from 'Hello, world!' to 'Hola, mundo!'

eth_chainId
eth_getTransactionByHash
eth_chainId
eth_getTransactionReceipt
eth_chainId
eth_call
  Contract call:       Greeter#greet
  From:                0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
  To:                  0x5fbdb2315678afecb367f032d93f642f64180aa3
```