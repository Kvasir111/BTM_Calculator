<template>
    <div>
      <div class="bg-white">
        <div :key="index" v-for="(week, index) in weeks">
          <h2 class="text-xl fontOpenSans">Week {{index +1}}</h2>
          <ul>
            <li :key="extersize" v-for="(extersize, index) in week.exercises">
              {{extersize.exerciseName}}: {{extersize.percentages}} {{weights[0].weight}}
            </li>
          </ul>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        name: "program",
      props : ['weights'],
      data : function () {
          return{
            weeks: [
              {week: '1', exercises: [
                  {exerciseName: 'Squat', percentages: [.70, .80, .90, .90, .90, .90, .90]},
                  {exerciseName: 'OHP', percentages: [.70, .80, .90, .70, .90,]},
                  {exerciseName: 'Chin-ups', percentages: ['Bodyweight']},
                  {exerciseName: 'Face Pulls/Band Pullaparts', percentages: [1]},
                  {exerciseName: 'Dips', percentages: ['Bodyweight']}
                ]
              }
            ]
          }
      }
    }
</script>

<style scoped>

</style>
