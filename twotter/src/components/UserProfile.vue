<template>
  <div class="user-profile">
    <div class="user-profile_sidebar">
      <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{ user.username }}</h1>
        <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile_follower-count">
          <strong> Followers: </strong> {{ followers }}
        </div>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot" />
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";
import CreateTwootPanel from "./CreateTwootPanel";
export default {
  name: "UserProfile",
  components: { CreateTwootPanel, TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_rjcrter11",
        firstName: "Rachel",
        lastName: "Carter",
        email: "rjcrter11@gmail.com",
        isAdmin: true,
        twoots: [
          {
            id: 1,
            content: "Twotter is amazing",
          },
          {
            id: 2,
            content: "Dont forget to subscribe to something or other.",
          },
        ],
      },
      methods: {
        addTwoot(twoot) {
          this.user.twoots.unshift({
            id: this.user.twoots.length + 1,
            content: twoot,
          });
        },
      },
    };
  },
};
</script>

<style scoped lang="scss">
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;

  .user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-bottom: auto;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;

    h1 {
      margin: 0;
    }

    .user-profile_admin-badge {
      background-color: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }
}
</style>