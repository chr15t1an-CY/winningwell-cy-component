<!-- put your html markup in the template tag -->
<template>
  <div class="custom-code-sample">
    <v-card>
      <v-card-text>
        <p> {{trigger_name}} Results!</p>
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
        <h1>Test</h1>
        <h5>The "ctx" prop</h5>
        <p>The ctx prop in the sample script above is a JavaScript object that provides your custom code a bunch of context about the learner taking the lesson and their progress, as well information about the lesson itself. Also, we include some organizational information as well. </p>

        <p>Check it out! Want to see what the ctx property has stored in it right now?</p>
        <v-btn @click="ctxHidden = !ctxHidden" color="primary">
          <span v-if="ctxHidden">View ctx property values</span>
          <span v-else>Hide ctx values</span>
        </v-btn>
        <pre v-if="!ctxHidden">{{ctx}}</pre>

        <h5 style="margin-top: 20px">Example of ctx Property Use</h5>
        <p>Hi {{learner.first_name}}! Here's your progress so far!</p>
        <h1 class="animated lightSpeedIn">Score: {{ctx.lessonStats.points}}</h1>
        <h1 class="animated lightSpeedIn">Completion: {{ctx.lessonStats.completedPerc}}%</h1>

        <h5 style="margin-top: 20px">Completion</h5>
        <p>Custom code creators have the ability to block the advancement of a lesson by choosing when to "emit" the "completed" event. Under methods in this sample, you will see a "complete" method that "emits" the "completed" event to the parent lesson only when you click the complete button below.</p>
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

//
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
        ctxHidden : true,
        trigger_name: this.ctx.lesson.name,
        email:this.ctx.learner.email,
        totalUserscore:8,
        fullName : [
          this.ctx.learner.first_name,
          this.ctx.learner.first_name
        ].join(' ')
      }
    },
    created: function() {
        console.log('.CTX Property');
        console.log('--------');
        console.log(this.ctx);


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
        this.$emit('completed');
      }
    },

    computed: {
      totalUserscore: function () {
        // loop through all items ctx.lesson.items
        // a.lesson.items;
        a = this.ctx;
        var points = Number(0);
        for (i = 0; i < a.lesson.items.length; i++) {
            // console.log(a.lesson.items[i]);
            item = a.lesson.items[i];
            points = points + Number(item.engagementState.points);
            // Count shaded twice.
            meta = item.values.metadata;
            if (meta['shadded']) {
              points = points + Number(item.engagementState.points);
            }

          }

        this.totalUserscore = points;
      },

      learner(){
        return this.ctx.learner;
      }
    },

    //DO NOT REMOVE. This emits to the parent lesson that your custom code is fully loaded
    mounted(){
      this.$emit('loaded')
      (function(g) {
            var ns, script, first;
            ns = 'Conveyour';
            g[ns] = g[ns] || {};
            g[ns].config = {
              domain: this.ctx.lesson.metadata['domain'],
              appkey: this.ctx.lesson.metadata['appkey'],
              token:  this.ctx.lesson.metadata['token']
            };
            g[ns].identify = function() { g[ns].q = g[ns].q || []; g[ns].q.push({m: 'identify', as: arguments}); };
            g[ns].track = function() { g[ns].q = g[ns].q || []; g[ns].q.push({m: 'track', as: arguments}); };
            script = document.createElement('script');
            script.type = 'text/javascript';
            script.async = true;
            script.src = 'https://app.conveyour.com/js/cdn/analytics.v1.min.js';
            first = document.getElementsByTagName('script')[0];
            first.parentNode.insertBefore(script, first);
          })(window);
      // var data = {};
      data['wwscore'] = this.totalUserscore;
           Conveyour.identify(this.email, data).done(function(data){
                 console.log(data)
               });

    },

  }
</script>
