<template>
  <div class="container-fluid">
    <div class="row" id="points"><div class="col-12">Unspent Points: {{points}}</div></div>
    
    <div class="row" id="strength">
      <div class="label col-md-6">Strength:</div>
      <div class="feats col-md-1">{{strength}}</div>
      <div class="points col-md-1">{{strengthPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeStrength(true)">+</button>
        {{(strength - strength % 5) / 5 + 1}}
        <button v-on:click="changeStrength(false)">-</button>
      </div>
    </div>

    <div class="row" id="agility">
      <div class="label col-md-6">Agility:</div>
      <div class="feats col-md-1">{{agility}}</div>
      <div class="points col-md-1">{{agilityPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeAgility(true)">+</button>
        {{(agility - agility % 5) / 5 + 1}}
        <button v-on:click="changeAgility(false)">-</button>
      </div>
    </div>

    <div class="row" id="vitality">
      <div class="label col-md-6">Vitality:</div>
      <div class="feats col-md-1">{{vitality}}</div>
      <div class="points col-md-1">{{vitalityPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeVitality(true)">+</button>
        {{(vitality - vitality % 5) / 5 + 1}}
        <button v-on:click="changeVitality(false)">-</button>
      </div>
    </div>

    <div class="row" id="accuracy">
      <div class="label col-md-6">Accuracy:</div>
      <div class="feats col-md-1">{{accuracy}}</div>
      <div class="points col-md-1">{{accuracyPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeAccuracy(true)">+</button>
        {{(accuracy - accuracy % 5) / 5 + 1}}
        <button v-on:click="changeAccuracy(false)">-</button>
      </div>
    </div>

    <div class="row" id="grit">
      <div class="label col-md-6">Grit:</div>
      <div class="feats col-md-1">{{grit}}</div>
      <div class="points col-md-1">{{gritPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeGrit(true)">+</button>
        {{(grit - grit % 5) / 5 + 1}}
        <button v-on:click="changeGrit(false)">-</button>
      </div>
    </div>

    <div class="row" id="encumberance">
      <div class="label col-md-6">Encumberance:</div>
      <div class="feats col-md-1">{{encumberance}}</div>
      <div class="points col-md-1">{{encumberancePoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeEncumberance(true)">+</button>
        {{(encumberance - encumberance % 5) / 5 + 1}}
        <button v-on:click="changeEncumberance(false)">-</button>
      </div>
    </div>

    <div class="row" id="survival">
      <div class="label col-md-6">Survival:</div>
      <div class="feats col-md-1">{{survival}}</div>
      <div class="points col-md-1">{{survivalPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeSurvival(true)">+</button>
        {{(survival - survival % 5) / 5 + 1}}
        <button v-on:click="changeSurvival(false)">-</button>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      strength: 0,
      strengthPoints: 0,

      agility: 0,
      agilityPoints: 0,

      vitality: 0,
      vitalityPoints: 0,

      accuracy: 0,
      accuracyPoints: 0,

      grit: 0,
      gritPoints: 0,

      encumberance: 0,
      encumberancePoints: 0,

      survival: 0,
      survivalPoints: 0,

      points: 389
    };
  },
  props: {
    msg: String
  },
  methods: {
    reverseMessage: function() {
      this.msg = this.msg
        .split("")
        .reverse()
        .join("");
    },

    pointCalculation: function(increment, current) {
      const cost = (current - current % 5) / 5 + 1;
      var newPoints = this.points;
      var newFeat = current;

      if (increment && current < 50 && this.points - cost >= 0) {
        newPoints -= cost;
        newFeat += 1;
      }

      if (!increment && newFeat > 0) {
        if (newFeat % 5 === 0) {
          newPoints += cost - 1;
        } else {
          newPoints += cost;
        }
        newFeat -= 1;
      }

      var spentPoints = 0;
      for (var i = 0; i < newFeat; i++) {
        var costSpent = ((i - i % 5) / 5) + 1;
        spentPoints += costSpent;
      }

      return { points: newPoints, feat: newFeat, cost: cost, spentPoints: spentPoints };
    },

    changeStrength: function(increment) {
      var newValues = this.pointCalculation(increment, this.strength);
      this.strength = newValues.feat;
      this.points = newValues.points;
      this.strengthPoints = newValues.spentPoints;
    },

    changeAgility: function(increment) {
      var newValues = this.pointCalculation(increment, this.agility);
      this.agility = newValues.feat;
      this.points = newValues.points;
      this.agilityPoints = newValues.spentPoints;
    },

    changeVitality: function(increment) {
      var newValues = this.pointCalculation(increment, this.vitality);
      this.vitality = newValues.feat;
      this.points = newValues.points;
      this.vitalityPoints = newValues.spentPoints;
    },

    changeAccuracy: function(increment) {
      var newValues = this.pointCalculation(increment, this.accuracy);
      this.accuracy = newValues.feat;
      this.points = newValues.points;
      this.accuracyPoints = newValues.spentPoints;
    },

    changeGrit: function(increment) {
      var newValues = this.pointCalculation(increment, this.grit);
      this.grit = newValues.feat;
      this.points = newValues.points;
      this.gritPoints = newValues.spentPoints;
    },

    changeEncumberance: function(increment) {
      var newValues = this.pointCalculation(increment, this.encumberance);
      this.encumberance = newValues.feat;
      this.points = newValues.points;
      this.encumberancePoints = newValues.spentPoints;
    },

    changeSurvival: function(increment) {
      var newValues = this.pointCalculation(increment, this.survival);
      this.survival = newValues.feat;
      this.points = newValues.points;
      this.survivalPoints = newValues.spentPoints;
    }
  }
};
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
