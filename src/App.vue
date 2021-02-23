<template>
  <div id="app">
    <header>
      <h1>Bank of CodeClan</h1>
      <h2>Total deposits: £{{ totalBalances }} </h2>
      <p>Total Deposits ☝️ should update dynamically when we add a new account.</p>
    </header>

    <form v-on:submit.prevent="saveAccount">
      <h3>Add a new Account</h3>
      <input placeholder="Name" type="text" v-model="newAccount.name" />
      <input type="number" v-model.number="newAccount.balance" />
      <input type="submit" value="Add Account"/>
    </form>

    <section>
      <div class="account" v-for="account in accounts">
        <h2>{{ account.name }}</h2>
        <p>Balance: £{{ account.balance }}</p>
      </div>
    </section>

    <form v-on:submit.prevent="filterAmount">
      <h3>Filter accounts by minimum amount</h3>
      <input type="number" placeholder="minimum balance" v-model.number="filterAmount" />
    </form>

    <section>
      <div class="account" v-for="account in filteredAccounts">
        <h2>{{ account.name }}</h2>
        <p>Balance: £{{ account.balance }}</p>
      </div>
    </section>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      accounts: [
        { name: "Daniella Ellicombe", balance: 600 },
        { name: "Barbara Rabson", balance: 750 },
        { name: "James Schofield", balance: 200 },
        { name: "Irma Diloway", balance: 1200 }
      ],
      newAccount: {
        name: "",
        balance: 0
      },
      filterAmount: 0
    }
  },
  computed: {
    totalBalances: function(){
      return this.accounts.reduce((runningTotal, account) => runningTotal + account.balance, 0);
    },
    filteredAccounts: function(){
      const filteredAccounts = this.accounts.filter(account => account.balance > this.filterAmount);
      return filteredAccounts
    }
  },
    methods: {
      saveAccount: function(){
        this.accounts.unshift(this.newAccount);

        this.newAccount = {
          name: "",
          balance: 0
        };
      }
    }
}
</script>

<style>
header {
  background: #eee;
  padding: 10px 20px;
  color: #333;
}

form, #filterInput {
  background: #eee;
  padding: 10px 20px 20px 20px;
  margin-top: 40px;
}

section {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}

.account {
  background: #eee;
  padding: 10px 20px;
  margin: 20px 0;
  width: 20%;
}

</style>
