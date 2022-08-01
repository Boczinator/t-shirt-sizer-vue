<template>
  <div class="flex flex-wrap justify-center">
    <form class="w-full max-w-xl" @submit.prevent="addNewTeamPlayer">
      <div class="flex items-center border-b border-teal-500 py-2">
        <input class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" id="name" placeholder="Team Player" v-model.trim="teamPlayer" />
        <button @click="addNewTeamPlayer" class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow" type="button">
          Add
        </button>
      </div>
    </form>

    <ul class="w-full flex flex-wrap">
      <li class="px-9 py-10 w-full lg:w-1/3" v-bind:key="item.id" v-for="(item, index) in teamPlayers">
        <form>
          <div class="text-2xl font-bold">{{ item.name }} ({{ item.hoursAvailable }} hours)</div>
          <input class="w-full h-1 bg-blue rounded outline-none slider-thumb" v-model="item.hoursAvailable" id="hours" type="range" value="80" min="1" max="120">

          <input class="uppercase bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded mx-2 my-1 cursor-pointer" type="button" v-for="size in sizes" v-bind:key="size.id" v-bind:value="size.name" @click="subtractHours(index, size.value); addHoursTag(index, size);">

          <div class="w-full">
            <button class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-full inline-flex items-center mx-1 my-1 uppercase cursor-pointer" type="button" v-for="(size, sizeIndex) in item.chosenSizes" v-bind:key="size.id" v-bind:value="size.name" @click="removeHoursTag(index, sizeIndex, size.value)">
              {{ size.name }}
              <svg class="fill-current w-4 h-4 ml-2" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 496 496" style="enable-background:new 0 0 496 496;" xml:space="preserve"><path style="fill:#B5092B;" d="M496,248c0,136.8-111.2,248-248,248S0,384.8,0,248S111.2,0,248,0S496,111.2,496,248z"/><path style="fill:#890027;" d="M248,0c136.8,0,248,111.2,248,248S384.8,496,248,496"/><path style="fill:#9B0025;" d="M72.8,72.8c96.8-96.8,253.6-96.8,350.4,0s96.8,253.6,0,350.4"/><g><path style="fill:#EEFFFF;" d="M321.6,333.6c-3.2,0-5.6-0.8-8-3.2l-148-148c-4.8-4.8-4.8-12,0-16.8s12-4.8,16.8,0l148,148c4.8,4.8,4.8,12,0,16.8C328,332.8,324.8,333.6,321.6,333.6z"/><path style="fill:#EEFFFF;" d="M174.4,333.6c-3.2,0-5.6-0.8-8-3.2c-4.8-4.8-4.8-12,0-16.8l148-148c4.8-4.8,12-4.8,16.8,0s4.8,12,0,16.8l-148.8,148C180,332.8,176.8,333.6,174.4,333.6z"/></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g></svg>
            </button>
          </div>
        </form>
        <button @click="deleteTeamPlayer(index)" v-if="teamPlayers.length" class="uppercase bg-transparent hover:bg-red-500 text-red-700 font-semibold hover:text-white py-2 px-4 border border-red-500 hover:border-transparent rounded mx-2 my-8 cursor-pointer">Delete Team Player</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'SizerItem',
  data() {
    return {
      teamPlayer: '',
      teamPlayers: [],
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
    addNewTeamPlayer() {
      this.teamPlayers.push({
        name: this.teamPlayer,
        hoursAvailable: 80,
        chosenSizes: []
      });
      this.teamPlayer = '';
    },
    subtractHours(index, hours) {
      this.teamPlayers[index].hoursAvailable = this.teamPlayers[index].hoursAvailable - hours;
    },
    addHoursTag(index, value) {
      this.teamPlayers[index].chosenSizes.push(value);
    },
    removeHoursTag(index, sizeIndex, hours) {
      this.teamPlayers[index].hoursAvailable = parseInt(this.teamPlayers[index].hoursAvailable) + parseInt(hours);
      this.teamPlayers[index].chosenSizes.splice(sizeIndex, 1);
    },
    deleteTeamPlayer(index) {
      this.teamPlayers.splice(index, 1);
    }
  }
}
</script>
