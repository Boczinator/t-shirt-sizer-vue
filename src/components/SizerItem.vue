<template>
  <div>
    <form @submit.prevent="addNewTeamMember">
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

          <input type="button" v-for="size in sizes" v-bind:key="size.id" v-bind:value="size.name" @click="subtractHours(index, size.value); addHoursTag(index, size);">

          <button type="button" v-for="(size, sizeIndex) in item.chosenSizes" v-bind:key="size.id" v-bind:value="size.name" @click="removeHoursTag(index, sizeIndex, size.value)">{{ size.name }} <span>X</span></button>
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
          name: 'xxl',
          value: 24
        }
      }
    }
  },
  methods: {
    addNewTeamMember() {
      this.teamMembers.push({
        name: this.name,
        hoursAvailable: 80,
        chosenSizes: []
      });
      this.name = '';
    },
    subtractHours(index, hours) {
      this.teamMembers[index].hoursAvailable = this.teamMembers[index].hoursAvailable - hours;
    },
    addHoursTag(index, value) {
      this.teamMembers[index].chosenSizes.push(value);
    },
    removeHoursTag(index, sizeIndex, hours) {
      this.teamMembers[index].hoursAvailable = this.teamMembers[index].hoursAvailable + hours;
      this.teamMembers[index].chosenSizes.splice(sizeIndex, 1);
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
