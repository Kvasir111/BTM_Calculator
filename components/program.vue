<template>
    <div>

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
