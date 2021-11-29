<template>
  <div>
    <form @submit.prevent="addNewName">
      <label for="name">Team Member </label>
      <input id="name" v-model.trim="name" />
    </form>

    <ul>
      <li>
        <form v-bind:key="item.id" v-for="(item, index) in teamMembers">
          <div>{{ item.name }}</div>
          <label for="hours">Hours</label>
          <input v-model="item.hoursAvailable" id="hours" type="range" value="80" min="1" max="120">
          <output>{{ item.hoursAvailable }}</output>

          <input type="button" v-for="size in sizes" v-bind:key="size.id" v-bind:value="size.name" @click="substractHours(index, size.value)">

          <input type="button" v-for="size in item.chosenSizes" v-bind:key="size.id" v-bind:value="size.name">
        </form>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'SizerItem',
  data() {
    return {
      teamMember: '',
      teamMembers: [],
      sizes: {
        'xs': {
          name: 'xs',
          value: 1
        },
        's': {
          name: 's',
          value: 2
        },
        'm': {
          name: 'm',
          value: 4
        },
        'l': {
          name: 'l',
          value: 8
        },
        'xl': {
          name: 'xl',
          value: 16
        },
        'xxl': {
          name: 'xl',
          value: 24
        }
      }
    }
  },
  methods: {
    addNewName() {
      this.teamMembers.push({
        name: this.name,
        hoursAvailable: 80,
        chosenSizes: []
      });
      this.name = '';
    },
    substractHours(value, hours) {
      this.teamMembers[value].hoursAvailable = this.teamMembers[value].hoursAvailable - hours;
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
