<template>
  <div>
    <!-- USER CARD -->
    <h2>Hello!</h2>
    <h5 class="mb-4">How are you doing today ?</h5>
    <v-card elevation="1" class="pa-2"> 
      <div class="d-flex justify-center align-center flex-column">
      <v-img 
        max-height="200" 
        max-width="25%" 
        src="https://cdn3.iconfinder.com/data/icons/business-avatar-1/512/8_avatar-512.png"
        lazy-src="https://picsum.photos/id/11/10/6"
      ></v-img>
      <strong class="username">{{ user.firstname }} {{ user.lastname }}</strong>
      <small>{{ user.email }}</small>
      </div>
    </v-card>

    <!-- CARDS PROFILE -->
    <div class="mt-4">
      <v-card 
        elevation="1" 
        ripple 
        class="pa-4 mb-2 d-flex align-center justify-space-between" 
        v-for="(item, index) in cards" 
        :key="index"
        @click="navigateTo(item)"
      >
        <!-- INFO -->
        <div class="d-flex">
          <v-icon color="black">{{ item.icon }}</v-icon>
          <div class="d-flex flex-column ml-4">
            <strong>{{ item.label }}</strong>
            <div class="small-text">{{ item.sublabel }}</div>
          </div>
        </div>

        <!-- ICON -->
        <div>
          <v-icon small color="black">keyboard_arrow_right</v-icon>
        </div>
        
      </v-card>
    </div>
    <v-btn class="mt-6" color="red" block outlined @click="logout">Sign Out</v-btn>
  </div>
</template>

<script>
export default {
  data: () => ({
    user: localStorage.getItem('user') && JSON.parse(localStorage.getItem('user')),
    cards: [
      { 
        label: 'Profile Details', 
        icon: 'person', 
        path: '/',
        sublabel: 'Change Your Profile Details'
      },
      { 
        label: 'Orders', 
        icon: 'local_shipping', 
        path: '/orders',
        sublabel: 'Check your order status'
      },
      { 
        label: 'Address', 
        icon: 'room', 
        path: '/address',
        sublabel: 'Save addresses for a hassle free checkout'
      }
    ]
  }),
  methods: {
    navigateTo(item) {
      this.$router.push({ path: item.path});
    },
    logout() {
      this.$store.dispatch('account/logout').then((path) => {
        if (path) {
          this.$router.push({ path });
          this.$store.commit('showSnackbar', { color: 'error', message: 'You have been logged out!' });
        }
      });
    }
  }
}
</script>

<style scoped lang="scss">
  .small-text {
    font-size : 12px;
  }
  .username {
    text-transform: capitalize;
  }
</style>