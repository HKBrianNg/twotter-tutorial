<template>
  <div class="user-profile"></div>
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{user.username}}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile_follower-count">
        <strong>Followers:</strong>{{followers}}
      </div>
      <div class="user-profile_twoots-wrapper">
        <!-- <div class="user-profile_twoot" v-for="twoot in user.twoots" :key="twoot.id">
          {{twoot.content}}
        </div> -->
        <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot"/>
      </div>

    </div>
</template>

<script>

import TwootItem from './TwootItem.vue';
export default {
  name: 'UserProfile',
  components: {
    TwootItem
  },
  data() {
    return {
      followers:0,
      user: {
        id: 1,
        username: 'ngshunchiang',
        firstName: 'Brian',
        lastName: 'Ng',
        email: 'ngshunchiang@hotmail.com',
        isAdmin: false,
        twoots: [
          {id:1, content: 'Twotter is Amazing'},
          {id:2, content: "Don't forget to subscriber to the Earth is Square!"},
        ]
      }
    }
  },
  watch: {
    followers(newfollowCount,oldfollowCount) {
      if (oldfollowCount < newfollowCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`
    },

    email() {
      return `email:${this.user.email}`
    }
  },
  methods: {
    followUser() {
      this.followers++;
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;  
  width:100%;
  padding:0px;
}

.user-profile_user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile_admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

.user-profile_twoots-wrapper {
 display: grid;
}
</style>
