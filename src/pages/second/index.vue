<template>
  <div class="container">
    <div v-if="wallet.address" class="account">
      <div class="balance">{{ wallet.balance }} ETH</div>
      <div class="address"><span>{{ formatAddress(wallet.address) }}</span>
        <Avatar :size="30"/>
      </div>
    </div>
    <button v-else class="btn" @click="handleClick">Connect Wallet</button>
  </div>

</template>

<style>
.btn {
  background-color: #F2E0E6FF;
  color: #cc0d62;
  padding: 10px 12px;
  border-radius: 20px;
  font-weight: 535;
  border: #f2edf0 2px solid;
}

.account {
  display: flex;
  justify-content: space-between;
  background-color: #f4f4f4;
  border: 2px #f4f4f4 solid;
  border-radius: 25px;
}

.account .balance {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 0.5rem;
}

.account .address {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #edeef0;
  height: 36px;
  border-radius: 25px;
  padding: 0 0.5rem;
  gap: 0.5rem;
}
</style>

<script lang="ts" setup>
import {ethers} from "ethers";
import {ref} from "vue";
import Avatar from "vue-boring-avatars";

const wallet = ref({"address": "", "balance": BigInt(0)})

const formatAddress = (address: string): string => {
  return address.substring(0, 6) + '...' + address.substring(address.length - 4)
}

const handleClick = async () => {
  try {
    const ethereum = (window as any).ethereum;
    const provider = new ethers.BrowserProvider(ethereum);
    const accounts = await ethereum.request({
      method: "wallet_requestPermissions",
      params: [{
        eth_accounts: {},
      }]
    }).then(() => ethereum.request({
      method: 'eth_requestAccounts'
    }))
    const balance = await provider.getBalance(accounts[0])
    wallet.value.address = accounts[0]
    wallet.value.balance = balance
  } catch (error) {
    console.log(error);
  }
}


</script>