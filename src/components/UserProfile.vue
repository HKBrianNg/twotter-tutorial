<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{user.username}}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile_follower-count">
        <strong>Followers:</strong>{{followers}}
      </div>
      <form class="user-profile_create-twoot" 
            @submit.prevent="createNewTwoot"
            :class="{'--exceed': newTwootCharacterCount > 180}"
        >
        <label for="newTwoot"><strong>New Twoot</strong>({{newTwootCharacterCount}}/180)</label>
        <textarea id="newTwoot" rows="4" v-model="newTwootContent">
        </textarea>
        <div class="user-profile_create-twoot-type">
          <label for="newTwootType"><strong>Type:</strong></label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
              {{option.name}}
            </option>
          </select>
        </div>
        <button>
          Twoot!
        </button>
      </form>
    </div>
    
    <div class="user-profile_twoots-wrapper">
        <!-- <div class="user-profile_twoot" v-for="twoot in user.twoots" :key="twoot.id">
          {{twoot.content}}
        </div> -->
        <TwootItem 
          v-for="twoot in user.twoots" 
          :key="twoot.id" 
          :username="user.username" 
          :twoot="twoot" 
          @favourite="toggleFavourite" />
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
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        { value: 'draft', name:'Draft'},
        { value: 'instant', name:'Instant Twoot'}
      ],
      followers:0,
      user: {
        id: 1,
        username: 'ngshunchiang',
        firstName: 'Brian',
        lastName: 'Ng',
        email: 'ngshunchiang@hotmail.com',
        isAdmin: true,
        twoots: [
          {id:1, content: 'Twotter is Amazing'},
          {id:2, content: "Don't forget to subscriber to the Earth is Square!"},
          {id:3, content: "test"},
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
    },

    newTwootCharacterCount() {
      return this.newTwootContent.length;
    }
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourited Tweet #${id}`);
    },
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !=='draft') {
        this.user.twoots.unshift( {
          id: this.user.twoots.length + 1,
          content: this.newTwootContent
        })
      this.newTwootContent='';
      }

    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style lang="scss" scoped>
.user-profile {
  /* display: grid;
  grid-template-columns: 1fr 3fr;   */
  width:100%;
  padding:0px;
  display: flex;
  flex-direction: row;
  .user-profile_user-panel {
    display: flex;
    flex: 1;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    .user-profile_admin-badge {
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
   

    .user-profile_create-twoot {
      display: flex;
      flex-direction: column;
      padding:20px;
      
      &.--exceed {
        color:red;
        button {
          background-color: red;
        }
      }
    }
  }
   .user-profile_twoots-wrapper {
      flex: 3;
      display: grid;
    }
}






</style>
