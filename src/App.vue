
<template>
  <div class="container mx-auto bg-gray-700 h-screen">
    <div class="h-12 bg-red-300 flex items-center">
      <p class="ml-2 text-xl">Phone Book hackajob challenge</p>
    </div>

    <div class="bg-red-300 w-full mt-23">
      <input @keyup="checkR" v-model="searchQuery" class="w-full h-24 p-2 outline-none" type="text" placeholder="search any contact" />

      <div>
        <div
          v-for="(n,i) in results"
          :key="i"
          class="mt-3 h-24 border-solid border-3 border-gray-600 shadow-lg flex items-center"
        >
          <div
            class="ml-3 h-12 w-12 border-solid border-2 border-gray-600 rounded-full flex items-center justify-center"
          >
            <p class="font-bold text-xl">{{n.name[0]}}</p>
          </div>

          <div class="ml-2">
            <p class="font-bold">{{n.name}}</p>
            <p>{{n.phone_number}}</p>
            <p>{{n.address}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      allPhone: [],
      results: [], //all phone book records will be stored here
      searchQuery:''
    };
  },
  created() {
    this.grabRecords();
  },
  methods: {
    checkR(){
      //check search query
      console.log(this.searchQuery)
    },
    async grabRecords() {
      let r = await axios.get(
        "http://www.mocky.io/v2/581335f71000004204abaf83"
      );

      if (r.status == 200) {
        //all is good
        this.allPhone = r.data.contacts;
        this.results = r.data.contacts;

        //sort in alphabetical order
        this.results.sort((a, b) => {
          if (a.name < b.name) {
            return -1;
          }
          if (a.name > b.name) {
            return 1;
          }
        });


      }
    }
  }
};
</script>