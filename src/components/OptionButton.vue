<template>
  <div class="buttons">
    <div>
      <img :src="getImage()" alt width="150" height="150" style="object-fit:contain;" />
    </div>
    <p class="heading">{{capatalize(this.data.id)}}</p>
    <div class="description">
      <p>{{shortenDescription(this.data.description)}}</p>
    </div>
    <div class="tag-section">
      <div class="tag" v-for="(tag, index) in this.data.tags" :key="index">
        <span>#{{tag}}</span>
      </div>
    </div>
    <div class="links">
      <button @click="homeItemSelected" class="btn buttonSelection">Cheatsheet</button>
      <button @click="openDocs()" class="btn buttonSelection">Documentation</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "OptionButton",
  props: {
    data: Object,
  },
  methods: {
    capatalize(value) {
      if (typeof value !== "string") return "";
      return value.charAt(0).toUpperCase() + value.slice(1);
    },
    homeItemSelected() {
      this.$emit("homeItemSelected", this.data.id);
    },
    shortenDescription(value) {
      if (value == null) return "";
      if (value.length > 90) return value.substring(0, 90) + "...";
      else return value;
    },
    openDocs() {
      window.open(this.data.url + "?ref=devsheets", "_blank");
    },
    getImage() {
      return require("../assets/" + this.data.image);
    },
  },
};
</script>

<style scoped>
.buttons {
  width: 300px;
  height: auto;
  border: 2px solid gray;
  margin: 20px 10px;
  padding-bottom: 10px;
  padding-top: 15px;
  padding-left: 5px;
  padding-right: 5px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  box-shadow: -5px 5px 10px #aaa;
}

.buttons:hover {
  width: 300px;
  height: auto;
  background-color: #fff;
  border: 2px solid black;
  margin: 10px;
  padding-bottom: 10px;
  padding-top: 15px;
  padding-left: 5px;
  padding-right: 5px;
  border-radius: 20px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  transform: translateY(-3%);
  transition: transform 0.4s ease-in-out;
}

.buttons .heading {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  margin-top: 5px;
}

.buttons .description {
  margin: 2px;
}

.buttons .description p {
  text-align: center;
}

.tag-section {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.tag {
  margin: 5px;
  padding: 2px 5px;
  font-size: 14px;
  font-weight: bold;
  border: 1px dashed black;
  background-color: #fff;
}

.links {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.buttonSelection {
  margin-left: 10px;
  margin-right: 10px;
  margin-top: 5px;
  margin-bottom: 5px;
  font-weight: bold;
  font-size: 15px;
  background-color: white;
  color: #cc0000ea;
  border: 1px solid #cc0000ea;
}

.buttonSelection:hover {
  margin-left: 10px;
  margin-right: 10px;
  margin-top: 5px;
  margin-bottom: 5px;
  font-weight: bold;
  font-size: 15px;
  background-color: #cc0000ea;
  color: white;
}

.buttonSelection:focus {
  box-shadow: none;
}
</style>