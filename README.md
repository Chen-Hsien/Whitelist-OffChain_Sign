# Sample Whitelist-OffChain_Sign

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a script that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat run scripts/deploy.js
```

過去建立的專案都是單頁的solidity直接在Remix上部署, 這邊練習用HardHat來進行開發.  
選擇了[alchemy-Off-Chain NFT Allowlist](https://docs.alchemy.com/docs/how-to-create-an-off-chain-nft-allowlist)專案來練習~  

專案內共一個SOL合約, 一個JS檔, 其中實作的技術則是digital signatures, [ECDSA橢圓曲線數位簽章算法](https://docs.openzeppelin.com/contracts/2.x/api/cryptography#ECDSA)  來避免將白名單直接儲存在鏈上造成高昂的GAS FEE.  

先看到Solidity的部分    
mint時檢查了兩個部分,以此作為白名單的設置  
1. mapping的 signatureUsed用來確認signature是否曾經使用過  
2. recoverSigner會將public address經由橢圓曲線加密後回傳signature是否與owner相等  

而JS的部分    
  
先定義allowlistedAddresses有哪些地址, 將白名單以off Chain的方式紀錄在本機不上鏈  
以此檢查錢包地址是否位於白名單中, 並將public address 與私鑰一起送給smart contract, 進行recover去認signer是否為contract的owner以前確認mint白單的所有者  
這樣就大功告成一個off chain的白單設計了！  
