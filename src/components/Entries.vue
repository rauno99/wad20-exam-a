<template>
  <div>
    <button @click="toggleBtn">{{ btnText }}</button>
    <li v-for="entry in sortedEntries" :key="entry">
      <h1>{{ entry.title }}</h1>
      <small>{{ entry.date | formatDate }}</small> <br>
      <img :src="entry.image">
      <p>{{ entry.text }}</p>
    </li>

  </div>
</template>

<script>
import moment from "moment"
export default {
  name: 'Entries',
  data: function () {
    return {
      btnText: "Newest to Oldest"
    }
  },
  props: {
    entries: Array
  },
  computed: {
    sortedEntries: function() {
      let array = this.entries.slice()
      array.sort((a, b) => {
        return new Date(b.date) - new Date(a.date);
      });
      if (this.btnText === "Newest to Oldest") {
        return array;
      }
      else {
        return array.reverse();
      }
    }
  },
  filters: {
    formatDate: function (date) {
      return moment(String(date)).format("LLLL");
    }
  },
  methods: {
    toggleBtn: function () {
      if (this.btnText === "Newest to Oldest") {
        this.btnText = "Oldest to Newest"
      }
      else {
        this.btnText = "Newest to Oldest"
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>