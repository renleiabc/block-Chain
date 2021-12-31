<template>
  <h1>理解开发HD 钱包涉及的 BIP32、BIP44、BIP39</h1>
  <div>
    <a href="https://learnblockchain.cn/2018/09/28/hdwallet/" target="_blank"
      >文章来源</a
    >
    <div class="eth">
      <div
        class="eth-item"
        v-for="(item, index) in list"
        :key="index"
        style="margin-bottom: 20px"
      >
        <div>{{ item.words }}</div>
        <div>{{ item.privateKey }}</div>
        <div>{{ item.address }}</div>
      </div>
      <button @click="handleaddOther">生成</button>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue';
import { hdkey } from 'ethereumjs-wallet';
import { ethers } from 'ethers';
const bip39 = require('bip39');
// 生成助记词
var util = require('ethereumjs-util');
const mnemonic = bip39.generateMnemonic(160);
const arrMne = mnemonic.split(' ');
console.log(mnemonic);
console.log(arrMne);
const words = `助记词：${mnemonic}`;
var seed = bip39.mnemonicToSeed(mnemonic, 'pwd');
var hdWallet = hdkey.fromMasterSeed(seed);

// eslint-disable-next-line quotes
var key1 = hdWallet.derivePath("m/44'/60'/0'/0");
var prKey = util.bufferToHex(key1._hdkey._privateKey);
console.log('私钥：' + prKey);
const privateKey = `私钥：${prKey.replace('0x', '')}`;
var address1 = util.pubToAddress(key1._hdkey._publicKey, true);
console.log(address1);
const address2 = util.bufferToHex(address1);
console.log('地址：' + address2);
const address = `地址：${address2}`;
console.log(address1.toString('hex'));
console.log('校验和地址：' + util.toChecksumAddress(address2));
const list = reactive([]);
console.log(list);
const listRelativeEffect = () => {
  const list = reactive([]);
  console.log(list);
  const addItemTolist = (item) => {
    console.log(item);
    list.push(item);
    console.log(list);
  };
  return { list, addItemTolist };
};
export default {
  setup() {
    const obj = {
      words,
      privateKey,
      address
    };
    const { list, addItemTolist } = listRelativeEffect();
    console.log(list);
    // addItemTolist(obj);
    console.log(obj);
    const obj1 = reactive(obj);
    addItemTolist(obj1);
    const handleAddEth = (obj1) => {
      console.log(obj1);
      addItemTolist(obj);
    };
    const handleaddOther = () => {
      const mnemonic = bip39.generateMnemonic(160);
      let seedBuffer = bip39.mnemonicToSeedSync(mnemonic);
      // let seedHex = seedBuffer.toString('hex');
      //  var seed = bip39.mnemonicToSeed(mnemonic);
      console.log(seed);
      console.log(ethers);
      let Wallet = ethers.Wallet.fromMnemonic(mnemonic);
      let privateKey1 = Wallet.privateKey;
      console.log('ETH私钥：', privateKey1);
      const words = `助记词：${mnemonic}`;
      var hdWallet = hdkey.fromMasterSeed(seedBuffer);
      console.log(hdWallet);
      var prKey1 = util.bufferToHex(hdWallet._hdkey._privateKey);
      console.log(prKey1);
      // eslint-disable-next-line quotes
      var key1 = hdWallet.derivePath("m/44'/60'/0'/0/0");
      console.log(key1);
      var prKey = util.bufferToHex(key1._hdkey._privateKey);
      console.log(prKey);
      const privateKey = `私钥：${prKey.replace('0x', '')}`;
      console.log(privateKey);
      var address1 = util.pubToAddress(key1._hdkey._publicKey, true);
      console.log(address1);
      const address2 = util.bufferToHex(address1);
      console.log('地址：' + address2);
      const address = `地址：${address2}`;
      const obj = {
        words,
        privateKey,
        address
      };
      list.push(obj);
    };
    return {
      handleAddEth,
      addItemTolist,
      list,
      obj1,
      handleaddOther
    };
  }
};
</script>
<style></style>
