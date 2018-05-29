<template>
  <div class="container">
    <div class="row" id="points"><div class="col-12">Unspent Points: {{points}} <button v-on:click="resetPoints()">Reset Points</button></div></div>
    
    <div class="row headers">
      <div class="col-md-6 text-left">Stat</div>
      <div class="col-md-1 text-left">Feats</div>
      <div class="col-md-1 text-left">Points</div>
    </div>

    <div class="row" id="strength">
      <div class="label col-md-6 text-left">Strength:</div>
      <div class="feats col-md-1 text-left">{{strength}}</div>
      <div class="points col-md-1 text-left">{{strengthPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeStrength(true)">+</button>
        {{(strength - strength % 5) / 5 + 1}}
        <button v-on:click="changeStrength(false)">-</button>
      </div>
    </div>

    <div class="row" id="agility">
      <div class="label col-md-6 text-left">Agility:</div>
      <div class="feats col-md-1 text-left">{{agility}}</div>
      <div class="points col-md-1 text-left">{{agilityPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeAgility(true)">+</button>
        {{(agility - agility % 5) / 5 + 1}}
        <button v-on:click="changeAgility(false)">-</button>
      </div>
    </div>

    <div class="row" id="vitality">
      <div class="label col-md-6 text-left">Vitality:</div>
      <div class="feats col-md-1 text-left">{{vitality}}</div>
      <div class="points col-md-1 text-left">{{vitalityPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeVitality(true)">+</button>
        {{(vitality - vitality % 5) / 5 + 1}}
        <button v-on:click="changeVitality(false)">-</button>
      </div>
    </div>

    <div class="row" id="accuracy">
      <div class="label col-md-6 text-left">Accuracy:</div>
      <div class="feats col-md-1 text-left">{{accuracy}}</div>
      <div class="points col-md-1 text-left">{{accuracyPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeAccuracy(true)">+</button>
        {{(accuracy - accuracy % 5) / 5 + 1}}
        <button v-on:click="changeAccuracy(false)">-</button>
      </div>
    </div>

    <div class="row" id="grit">
      <div class="label col-md-6 text-left">Grit:</div>
      <div class="feats col-md-1 text-left">{{grit}}</div>
      <div class="points col-md-1 text-left">{{gritPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeGrit(true)">+</button>
        {{(grit - grit % 5) / 5 + 1}}
        <button v-on:click="changeGrit(false)">-</button>
      </div>
    </div>

    <div class="row" id="encumberance">
      <div class="label col-md-6 text-left">Encumberance:</div>
      <div class="feats col-md-1 text-left">{{encumberance}}</div>
      <div class="points col-md-1 text-left">{{encumberancePoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeEncumberance(true)">+</button>
        {{(encumberance - encumberance % 5) / 5 + 1}}
        <button v-on:click="changeEncumberance(false)">-</button>
      </div>
    </div>

    <div class="row" id="survival">
      <div class="label col-md-6 text-left">Survival:</div>
      <div class="feats col-md-1 text-left">{{survival}}</div>
      <div class="points col-md-1 text-left">{{survivalPoints}}</div>
      <div class="point-buttons col-md-4">
        <button v-on:click="changeSurvival(true)">+</button>
        {{(survival - survival % 5) / 5 + 1}}
        <button v-on:click="changeSurvival(false)">-</button>
      </div>
    </div>

    <div class="row stats">
      <div class="col-md-7">
        <div class="row">
          <div class="col-12"><p>Computed stats</p></div>
        </div>
        <div class="row meele">
          <div class="col-md-4 text-left">Base meele damage: 40</div>
          <div class="col-md-4 text-left">From strength: {{40 * ((strength * 2) / 100)}} ({{strength * 2}}%) </div>
          <div class="col-md-4 text-left">Total: {{(40 * ((strength * 2) / 100)) + 40}}</div>
        </div>

        <div class="row ranged">
          <div class="col-md-4 text-left">Base ranged damage: 40</div>
          <div class="col-md-4 text-left">From accuracy: {{40 * ((accuracy * 2) / 100)}} ({{accuracy * 2}}%) </div>
          <div class="col-md-4 text-left">Total: {{(40 * ((accuracy * 2) / 100)) + 40}}</div>
        </div>

        <div class="row armor">
          <div class="col-md-4 text-left">From agility: {{agility * 2}}</div>
          <div class="col-md-4 text-left">Damage Reduction: {{(agility * 2) * 0.28}}%</div>
          <div class="col-md-4 text-left">Total: {{agility * 2}}</div>
        </div>

        <div class="row health">
          <div class="col-md-4 text-left">Base health: 200</div>
          <div class="col-md-4 text-left">From vitality: {{vitality * 8}}</div>
          <div class="col-md-4 text-left">Total: {{vitality * 8 + 200}}</div>
        </div>

        <div class="row stamina">
          <div class="col-md-4 text-left">Base stamina: 100</div>
          <div class="col-md-4 text-left">From grit: {{grit * 3}} </div>
          <div class="col-md-4 text-left">Total: {{grit * 3 + 100}}</div>
        </div>

        <div class="row encumberance">
          <div class="col-md-4 text-left">Base encumberance: 70</div>
          <div class="col-md-4 text-left">From encumberance: {{encumberance * 7}}</div>
          <div class="col-md-4 text-left">Total: {{encumberance * 7 + 70}}</div>
        </div>

      </div>

      <!--
      <div class="col-md-5">
        <div class="row">
          <div class="col-12"><p>Feats from gear <button>Reset Gear</button></p></div>
        </div>

        <div class="row">
          <div class="col-12"><input type="text" placeholder="0"></div>
        </div>

        <div class="row">
          <div class="col-12"><input type="text" placeholder="0"></div>
        </div>

        <div class="row">
          <div class="col-12"><input type="text" placeholder="0"></div>
        </div>

        <div class="row">
          <div class="col-12"><input type="text" placeholder="0"></div>
        </div>
      </div>
      -->
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

      points: 390
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

    resetPoints() {
      this.strength = 0;
      this.strengthPoints = 0;
      this.agility = 0;
      this.agilityPoints = 0;
      this.vitality = 0;
      this.vitalityPoints = 0;
      this.accuracy = 0;
      this.accuracyPoints = 0;
      this.grit = 0;
      this.gritPoints = 0;
      this.encumberance = 0;
      this.encumberancePoints = 0;
      this.survival = 0;
      this.survivalPoints = 0;
      this.points = 390;
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
        var costSpent = (i - i % 5) / 5 + 1;
        spentPoints += costSpent;
      }

      return {
        points: newPoints,
        feat: newFeat,
        cost: cost,
        spentPoints: spentPoints
      };
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

.stats {
  margin-top: 3em;
}
</style>
