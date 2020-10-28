<template>
  <form
    class="create-twoot-panel"
    :class="{ '--exceeded': newTwootCharacterCount > 180 }"
    @submit.prevent="createNewTwoot"
  >
    <label for="newTwoot">
      <strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180)
    </label>
    <textarea id="newTwoot" rows="4" v-model="newTwootContent" />
    <div class="create-twoot-panel_submit">
      <div class="create-twoot-type">
        <label for="newTwootType"> <strong>Type: </strong> </label>
        <select id="newTwootType" v-model="selectedTwootType">
          <option
            :value="option.value"
            v-for="(option, idx) in twootTypes"
            :key="idx"
          >
            {{ option.name }}
          </option>
        </select>
      </div>
      <button>Twoot it!</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "CreateTwootPanel",
  data() {
    return {
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],

      computed: {
        newTwootCharacterCount() {
          return this.newTwootContent.length;
        },
      },
      methods: {
        createNewTwoot() {
          if (
            this.newTwootContent &&
            this.selectedTwootType !== "draft"
            // && this.newTwootCharacterCount <= 180
          ) {
            this.$emit("add-twoot", this.newTwootContent);
            this.newTwootContent = "";
          }
          //   else if (this.newTwootCharacterCount > 180) {
          //     alert("Character count must be 180 characters or fewer!");
          //   }
        },
      },
    };
  },
};
</script>

<style lang="scss" scoped>
.create-twoot-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;

  textarea {
    border: 1px solid #dfe3e8;
    border-radius: 5px;
  }
  .create-twoot-panel_submit {
    display: flex;
    justify-content: space-between;

    .create-twoot-type {
      padding: 10px 0;
    }
    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
    }
  }
  &.--exceeded {
    color: red;
    border-color: red;
    .create-twoot-panel__submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style> 