<!-- put your html markup in the template tag -->
<template>
  <div class="custom-code-sample">
    <v-card>
      <v-card-text>
        <h2> {{trigger_name}} Results!</h2>
        <p>Total Score => {{totalUserscore}}</p>
        <p>Number of Shaded A's => {{numOfShadedAs}}</p>

        <p v-if="totalUserscore < 3">You probably experience lots of stress, bouncing back and forth between Gamer attempts to keep your job and frustration with your staff.</p>
        <p v-else-if="totalUserscore == 3">You likely do try to achieve results, but with a high degree of frustration common to the User style. You may try to be liked, but it generally doesn't work.</p>
        <p v-else-if="totalUserscore == 4 && numOfShadedAs < 1">You may identify with the Pleaser style, putting lots of effort into being liked and reacting to one crisis after anouther.</p>
        <p v-else-if="totalUserscore == 4 && numOfShadedAs >= 1">You probably are a results-oriented manager with an opportunity to sustain your results as you connect with and invest in your people.</p>
        <p v-else-if="totalUserscore == 5">You have Winning Well management instincts that likely get buried in day-to-day stress and personal frustrations.</p>
        <p v-else-if="totalUserscore == 6 && numOfShadedAs <= 2">You may identify with the Pleaser style, putting lots of effort into being liked and reacting to one crisis after anouther with some focus on results.</p>
        <p v-else-if="totalUserscore == 6 && numOfShadedAs >= 3">You likely have Winning Well instincts and a focus on results.</p>
        <p v-else-if="totalUserscore == 7">You likely have Winning Well instincts and focus on relation-ships. </p>
        <p v-else-if="totalUserscore == 8">You likely have strong Winning Well practices and may flex easily between results and relationships.</p>
        <p v-else-if="totalUserscore > 8">You likely have strong Winning Well practices and emphasize relationships in your day-today work. </p>
        <div v-else>
          Hmm. This is puzzling. I had trouble calculating your score. It could be an error on my end.
        </div>
        <hr/>

        <h5 style="margin-top: 20px">Mark Complete</h5>
        <v-btn color="primary" @click="complete">complete</v-btn>
      </v-card-text>
    </v-card>
  </div>
</template>

<!-- put your styles in the style tag. -->
<style scoped>
  .custom-code-sample p, .custom-code-sample ul{
    font-size: 16px;
  }
</style>

<!-- put your javascript / vue.js logic into your script tag -->
<!-- lang='es6' is important. Please include -->
<script lang='es6'>
  //your code should be exported using the module.exports object
  module.exports = {

    //give your custom code component a unique name, no spaces, camelCase
    name : 'CustomWw',
    //props are properties passed from the parent lesson context
    //into your component. Please always include this line
    //@ctx = the lesson context object
    //@ui = all of the ui vue components (see beforeMount)
    //@api = methods exposed to your code like updateLearner() giving you the ability
    //       to update a learner's profile in ConveYour from YOUR code
    props : [ 'ctx', 'ui', 'api' ],

    //the data function must return an object. Data values
    //return here can be used in your templates like this Hi {{fullName}}
    data(){
      return {
        trigger_name: this.ctx.lesson.name,
        email:this.ctx.learner.email,
        score:0,
      }
    },
    created: function() {
    },

    //this attaches the parent lesson ui components to your custom code
    //so that you can use built in lesson vue components in YOUR code!
    beforeMount(){
      this.$options.components = this.ui;

    },

    //methods are actions that occur as a result of clicking on items
    //see @click='complete' on the complete button in the template
    methods: {
      //emit an event to the parent lesson telling the lesson that the learner
      //interacting with this code has completed the interaction. By giving you
      //the power to signal when the learner is completed you can control the learner's
      //ability to progress through the rest of the lesson!
      complete(){
        //Emit compleated.
        this.$emit('completed');
        //Pass the score to the users contact record.
        this.api.updateLearner({ wwscore1 : Number(this.totalUserscore) });
      }
    },

    computed: {
      learner(){
        return this.ctx.learner;
      },
      totalUserscore(){
        // store the user value
        var a = this.ctx;
        // Insure points is an integer.
        var points = Number(0);
        //Grab Shadded A's (They are added twice.)
        var numOfShadedAs = this.numOfShadedAs;
        // Loop through lessons to compleate points.
        for (var i = 0; i < a.lesson.items.length; i++) {
            var item = a.lesson.items[i];
            points = points + Number(item.engagementState.points);
          }
        //Sum Points.
        var totalpoints = points+numOfShadedAs;
        //Set as score.
        self.score = totalpoints;

        return totalpoints;
      },
      numOfShadedAs(){
        // store the user value
        var a = this.ctx;
        // Insure points is an integer.
        var points = Number(0);
        // Insure points is an integer.
        var numOfShadedAs = Number(0);
        //Loop through and count shaded.
        for (var i = 0; i < a.lesson.items.length; i++) {
            var item = a.lesson.items[i];
            var meta = item.values.metadata;
            if (meta['shaded']) {
              numOfShadedAs = numOfShadedAs + Number(item.engagementState.points);
            }

          }
        //Return Shaded A's  
        return numOfShadedAs;
      },
    },

    //DO NOT REMOVE. This emits to the parent lesson that your custom code is fully loaded
    mounted(){
      this.$emit('loaded');

    },

  }
</script>
