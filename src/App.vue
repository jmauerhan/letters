<template>
  <v-app>
    <v-content>
      <v-container fluid>
        <v-slide-y-transition mode="out-in">
          <v-layout column align-center>
            <h1 style="font-size: 10vh">"{{sentence}}"
              <v-btn @click="backspace">Backspace</v-btn>
            </h1>
            <v-carousel style="height: 65vh" :cycle="false" v-model="picked" :hide-delimiters="true">
              <v-carousel-item v-for="(item,i) in opt" :key="i" @click="choose(item)">
                <h1 style="font-size: 50vh">{{item}}</h1>
              </v-carousel-item>
            </v-carousel>
          </v-layout>
        </v-slide-y-transition>
        <v-layout row wrap>
          <v-flex v-for="(item,i) in opt" :key="i" @click="scrollTo(i)">
            <v-btn>{{item}}</v-btn>
          </v-flex>
        </v-layout>

      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import _ from "lodash";

export default {
  data() {
    return {
      picked: 0,
      sentence: ""
    };
  },
  computed: {
    opt() {
      let alpha = " abcdefghijklmnopqrstuvwxyz".toUpperCase().split("");
      let num = _.range(0, 10);
      let words = ["YES ", "NO "];
      return alpha.concat(num).concat(words);
    }
  },
  methods: {
    choose(item) {
      console.log(item);
      this.sentence += item;
    },
    scrollTo(i) {
      this.picked = i;
    },
    backspace() {
      this.sentence = this.sentence.slice(0, -1);
    }
  }
};
</script>


<style>
h1 {
  cursor: pointer;
}
</style>