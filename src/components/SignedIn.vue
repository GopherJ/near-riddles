<template>
  <div>
    <button class="link" style="float: right" v-on:click="logout">Sign out</button>
    <main>
      <h1>
        Signed as: {{ accountId }}
      </h1>
    </main>
  </div>
</template>

<script>
import { logout } from "../utils"

export default {
  name: "SignedIn",
  computed: {
    isSignedIn() {
      return window.walletConnection? window.walletConnection.isSignedIn(): false
    },
    accountId() {
      return window.accountId
    },
    contractId() {
      return window.contract? window.contract.contractId: null
    },
    networkId() {
      return window.networkId
    },
  },

  methods: {
<<<<<<< Updated upstream
    retrieveSavedGreeting() {
      //retrieve greeting
      window.contract
        .get_greeting({ account_id: window.accountId })
        .then((greetingFromContract) => {
          this.savedGreeting = greetingFromContract
          this.newGreeting = greetingFromContract
        })
    },

    saveGreeting: async function (event) {
      // fired on form submit button used to update the greeting

      // disable the form while the value gets updated on-chain
      this.$refs.fieldset.disabled = true

      try {
        
        // make an update call to the smart contract
        await window.contract.set_greeting({
          // pass the new greeting
          message: this.newGreeting,
        })
      } catch (e) {
        alert(
          "Something went wrong! " +
            "Maybe you need to sign out and back in? " +
            "Check your browser console for more info."
        )
        throw e //re-throw
      } finally {
        // re-enable the form, whether the call succeeded or failed
        this.$refs.fieldset.disabled = false
      }

      // update savedGreeting with persisted value
      this.savedGreeting = this.newGreeting

      this.notificationVisible = true //show new notification

      // remove Notification again after css animation completes
      // this allows it to be shown again next time the form is submitted
      setTimeout(() => {
        this.notificationVisible = false
      }, 11000)

    },

    logout: logout,
=======
    logout,
>>>>>>> Stashed changes
  },
}
</script>
