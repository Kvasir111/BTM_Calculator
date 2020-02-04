<template>
  <div class="h-screen flex bg-black">
    <div class="m-auto bg-white rounded p-2 w-full sm:w-1/3" id="mainDiv">
      <form id="programEntry">
        <h1 class="text-2xl">{{realMaxTitle}}</h1>
        <h2 class="italic">{{realMaxDescription}}</h2>
        <div  class="text-center" key=index v-for="(lift, index) in maxes">
        <input
        v-bind:placeholder="lift.lift"
        v-bind:id="lift.lift"
               v-model="lift.weight"
        class="text-center mx-auto w-1/2 sm:w-1/3 border-b-2 border-black outline-none p-2">
          x
        <input
               placeholder="Reps"
               v-bind:id="lift.lift + ' reps'"
               v-model="lift.reps"
               class="inline text-center mx-auto w-1/2 sm:w-1/3 border-b-2 border-black outline-none p-2">
        <input>
        </div>
        <div class="mx-auto text-center p-2">
        <select class="border-b-2 border-black outline-none">
          <option disabled>Select weight Schema</option>
          <option :key="index" v-for="(system, index) in weightSystem" v-model="weightSystem">{{system.name}}</option>
        </select>
        </div>
        <div class="mx-auto text-center p-2">
          <button id="calculateButton" class="bg-red-600 py-2 px-2 rounded text-center italic font-bold" type="button" v-on:click="calculateProgram">Calculate Program</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>

export default {
  components: {

  },
  computed:{

  },
  data() {
    return {
      //These are the "Real Rep Maxes" meaning that weight you hit once in a blue moon
      realMaxTitle : 'Enter your real 1RMs (one rep maxes)',
      realMaxDescription: 'These will be used to calculate your Wendler TMs',
      maxes :  [
        {lift: "OHP", weight: "", reps: ''},
        {lift: "Squat", weight: "", reps: ''},
        {lift: "Bench", weight: "", reps: ''},
        {lift: "Deadlift", weight: "", reps: ''},
      ],
      //User can select the bar weight
      barWeight: '45',
      //these are the Wendler "Training Maxes" that are 90% of the 1RM that the user entered
      trainingMaxes: [
        {lift: "OHP", weight: ''},
        {lift: "Squat", weight: ''},
        {lift: "Bench", weight: ''},
        {lift: "Deadlift", weight: ''},
      ],
      weightSystem: [
        {name: 'Imperial', measurement: 'lbs'},
        {name: 'Metric', measurement: 'kgs'},
      ],
      //rounds the weight to the nearest 5lbs or 1kg
      rounding: true,

      weeks: [],
    }
  },
  methods : {
    //this method is if the user wants to enter a different bar weight
    setBarWeight(weight){
      this.barWeight = weight;
    },
    //May or may not be used, but if the user want to use a different weight type, this can be used to convert between the two
    convertWeight(weightSystem, weight){
      if (weightSystem === 'kgs'){
        return  (weight * (1/2.2046));

      }
      else if (weightSystem === 'lbs'){
        return  weight * 2.2046;
      }
    },
    //this is a formula that will be used to set the right 1RM if the user doesn't actually know their 1RM
    calculateRM(){
      for (let i = 0 ; i < this.maxes.length ; i++){
        if (this.maxes[i].reps > 1){
          this.maxes[i].weight = ((this.maxes[i].weight * 1.1307) + .6998);
        }
      }
    },
    //this calculates the Wendler TM's
    calculateTM(){
      for (let i = 0 ; i < this.trainingMaxes.length ; i++){
        this.trainingMaxes[i].weight =  (this.maxes[i].weight * .90);
        console.log(this.trainingMaxes[i].weight)
      }
    },
    //this is called when the user submits the form, it creates the entire 6 week program
    calculateProgram(){
      this.calculateRM();
      this.calculateTM();
    }

  }
}
</script>

<style>

</style>
