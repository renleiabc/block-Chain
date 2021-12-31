<template>
  <div class="private">
    <div class="private-item">
      <pre class="mark">
        import { ethers } from 'ethers';
        const bip39 = require('bip39');
        const mnemonic = bip39.generateMnemonic(160);
        console.log(mnemonic);
        let Wallet = ethers.Wallet.fromMnemonic(mnemonic);
        let privateKey = Wallet.privateKey.replace('0x', '');
        console.log('ETH私钥：', privateKey);
        let Wallet = ethers.Wallet.fromMnemonic(phrase);
        let privateKey = Wallet.privateKey.replace('0x', '');
        let publicKey = Wallet.publicKey.replace('0x', '');
        console.log('ETH私钥：', privateKey);
        console.log('ETH公钥：', publicKey);
        // 压缩公钥
        let compressedPublicKey = Wallet._signingKey().compressedPublicKey;
        console.log('压缩ETH公钥：', compressedPublicKey);
      </pre>
    </div>
    <div class="private-item">
      <pre class="mark">
        const bip39 = require('bip39');
        import { hdkey } from 'ethereumjs-wallet';
        const util = require('ethereumjs-util');
        const mnemonic = bip39.generateMnemonic(160);
        let seedBuffer = bip39.mnemonicToSeedSync(mnemonic);
    const hdWallet = hdkey.fromMasterSeed(seedBuffer);
    console.log(hdWallet);
    const prKey1 = util.bufferToHex(hdWallet._hdkey._privateKey);
    console.log(prKey1);
    // eslint-disable-next-line quotes
    const key1 = hdWallet.derivePath("m/44'/60'/0'/0/0");
    console.log(key1);
    const prKey = util.bufferToHex(key1._hdkey._privateKey).replace('0x', '');
    const pubKey = util.bufferToHex(key1._hdkey._publicKey).replace('0x', '');
    console.log(prKey);
    const privateKey2 = `私钥：${prKey}`;
    console.log(privateKey2);
    const publicKey2 = `压缩的公钥：${pubKey}`;
    console.log(publicKey2);
    console.log(pubKey === compressedPublicKey);
    console.log(prKey === privateKey);
    const address2 = util.pubToAddress(key1._hdkey._publicKey, true);
    console.log(address2);
    const address3 = util.bufferToHex(address2);
    console.log('地址：' + address3);
      </pre>
    </div>
    <button class="">生成</button>
  </div>
</template>
<script>
// eslint-disable-next-line no-unused-vars
import { hdkey } from 'ethereumjs-wallet';
const util = require('ethereumjs-util');
// eslint-disable-next-line no-unused-vars
const bitcoin = require('bitcoinjs-lib');
import { ethers } from 'ethers';
const bip39 = require('bip39');
export default {
  setup() {
    const mnemonic = bip39.generateMnemonic(160);
    console.log(mnemonic);
    // let phrase = ethers.Wallet.createRandom().mnemonic.phrase;
    //  console.log(phrase);
    let Wallet = ethers.Wallet.fromMnemonic(mnemonic);
    let privateKey = Wallet.privateKey.replace('0x', '');
    let publicKey = Wallet.publicKey.replace('0x', '');
    console.log('ETH私钥：', privateKey);
    console.log('ETH公钥：', publicKey);
    let address = Wallet.address;
    console.log('ETH地址：', address);
    console.log(Wallet._signingKey());
    // 压缩公钥
    let compressedPublicKey = Wallet._signingKey().compressedPublicKey.replace(
      '0x',
      ''
    );
    console.log('压缩ETH公钥：', compressedPublicKey.trim());
    /* let newWallet = ethers.Wallet.createRandom();
    let mnemonic1 = newWallet.mnemonic;
    console.log('mnemonic1:', mnemonic1);
    let address1 = newWallet.address;
    console.log('address1:', address1);
    let privateKey1 = newWallet.privateKey;
    console.log('privateKey1:', privateKey1);
    let compressedPublicKey1 = newWallet._signingKey().compressedPublicKey;
    console.log('publicKey:', compressedPublicKey1); */
    let seedBuffer = bip39.mnemonicToSeedSync(mnemonic);
    const hdWallet = hdkey.fromMasterSeed(seedBuffer);
    console.log(hdWallet);
    const prKey1 = util.bufferToHex(hdWallet._hdkey._privateKey);
    console.log(prKey1);
    // eslint-disable-next-line quotes
    const key1 = hdWallet.derivePath("m/44'/60'/0'/0/0");
    console.log(key1);
    const prKey = util.bufferToHex(key1._hdkey._privateKey).replace('0x', '');
    const pubKey = util.bufferToHex(key1._hdkey._publicKey).replace('0x', '');
    console.log(prKey);
    const privateKey2 = `私钥：${prKey}`;
    console.log(privateKey2);
    const publicKey2 = `压缩的公钥：${pubKey}`;
    console.log(publicKey2);
    console.log(pubKey === compressedPublicKey);
    console.log(prKey === privateKey);
    const address2 = util.pubToAddress(key1._hdkey._publicKey, true);
    console.log(address2);
    const address3 = util.bufferToHex(address2);
    console.log('地址：' + address3);
  }
};
</script>
