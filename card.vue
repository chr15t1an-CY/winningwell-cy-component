<!-- put your html markup in the template tag -->
<template>
  <div class="custom-code-sample">
    <v-card>
      <v-card-text>
        <h2> {{trigger_name}} Results!</h2>
        <p>Total Score {{totalUserscore}}</p>
        <p v-if="totalUserscore < 3">GAMER TENDENCIES Work may feel like a game you can't win. You probably experience lots of stress, bouncing back and forth between Gamer attempts to keep your job and frustration with your staff. To decrease your stress and increase your productivity, begin by reconnecting with yourself. What does your group exist to achieve? How can you connect to your people and the purpose in what you do? See Winning Well Chapter 10. To connect with people, try a listening tour. What is important to your people? What do they appreciate about their work? See Winning Well Chapters 12, 15, and 21.</p>
    <p v-else-if="totalUserscore == 3">USER TENDENCIES You likely do try to achieve results, but with a high degree of frustration common to the User style. You may try to be liked, but it generally doesn't work. You will see more productivity and less stress as you connect with your team, invest in them, and collaborate. See Winning Well Chapters 10, 12, 13, 14, and 16 to release their energy, create confidence and momentum, and get the feedback you need. Another way you can connect and collaborate with your team is to build ownership of decisions and problem solving. See Chapters 6 and 8.</p>
    <p v-else-if="totalUserscore == 4 && numOfShadedAs < 1">PLEASER TENDENCIES You may identify with the Pleaser style, putting lots of effort into being liked and reacting to one crisis after another. It can be exhausting. Examine your shared commitments. Can everyone on the team consistently and clearly answer what success looks like for their role, the team, and the organization? See Winning Well Chapter 4. If so, be sure to include accountability and celebration in how you end your meetings and delegate assignments. See Chapters 5 and 9.</p>
    <p v-else-if="totalUserscore == 4 && numOfShadedAs >= 1">USER TENDENCIES You probably are a results-oriented manager with an opportunity to sustain your results as you connect with and invest in your people. To decrease your stress and increase your productivity, begin by reconnecting with yourself. What does your group exist to achieve? What about your work is meaningful? How can you connect to your people and the purpose in what you do? See Winning Well Chapter 10. To connect with people, try a listening tour. What is important to your people? What do they appreciate about their work? See Winning Well Chapters 12, 15, and 21.</p>
    <p v-else-if="totalUserscore == 5">FRUSTRATED WINNING WELL You have Winning Well management instincts that likely get buried in day-to-day stress and personal frustrations. To start reclaiming your time and your team's productivity, establish clear personal priorities with your personal most important task. See Winning Well Chapter 10. Then establish clarity about what success looks like for your team and each individual person. See Winning Well Chapter 4. When you get clear about what you're doing and why you're doing it, your confidence will soar and fewer distractions will interrupt you.</p>
    <p v-else-if="totalUserscore == 6 && numOfShadedAs <= 2">PLEASER TENDENCIES You may identify with the Pleaser style, putting lots of effort into being liked and reacting to one crisis after another with some focus on results. Examine your shared commitments. Can everyone on the team consistently and clearly answer what success looks like for their role, the team, and the organization? See Winning Well Chapter 4. If so, be sure to include accountability and celebration in how you end your meetings and delegate assignments. See Chapters 5 and 9.</p>
    <p v-else-if="totalUserscore == 6 && numOfShadedAs >= 3">WINNING WELL TENDENCIES You likely have Winning Well instincts and a focus on results. Continue to connect, invest in, and collaborate with your people. You may want to schedule these activities to ensure they don't get left behind in the business of day-to-day work. See Winning Well Chapters 12, 17, 19, and 20. As you invest in people, be sure to find out what is meaningful to them and what kind of growth is most motivating for them.</p>
    <p v-else-if="totalUserscore == 7">WINNING WELL TENDENCIES You likely have Winning Well instincts and focus on relationships. To build on your foundation, examine your shared commitments. Can everyone on the team consistently and clearly answer what success looks like for their role, the team, and the organization? See Winning Well Chapter 4. If so, be sure to include accountability and celebration in how you end your meetings and delegate assignments. See Chapters 5 and 9.</p>
    <p v-else-if="totalUserscore == 8">WINNING WELL You likely have strong Winning Well practices and may flex easily between results and relationships. Where else can you use your strengths? What is the vision that will inspire you and your team for the year ahead? Maintain vigilance for the environmental changes and disruptive influences that can derail your healthy leadership. Continue to invest in your people and build leaders who will be able to maintain results in your absence. Help the growing leaders on your team develop their Winning Well skills. It's time to pass on your Winning Well skills to your team members. Build leaders by allowing them to lead meetings. See Winning Well Chapter 4, 5, and 6, practice connecting the what to the why. See Chapter 15. Lead with healthy recognition and celebration. See Chapter 20.</p>
    <p v-else-if="totalUserscore > 8">WINNING WELL You likely have strong Winning Well practices and emphasize relationships in your day-today work. Where else can you use your strengths? What is the vision that will inspire you and your team for the year ahead? Maintain vigilance for the environmental changes and disruptive influences that can derail your healthy leadership. Continue to invest in your people and build leaders who will be able to maintain results in your absence. Help the growing leaders on your team develop their Winning Well skills. It's time to pass on your Winning Well skills to your team members. Build leaders by allowing them to lead meetings. See Winning Well Chapter 4, 5, and 6, practice connecting the what to the why. See Chapter 15. Lead with healthy recognition and celebration. See Chapter 20.</p>
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
        this.api.updateLearner({ wwscore : Number(this.totalUserscore) });
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
