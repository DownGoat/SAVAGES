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
      <div class="feats col-md-1 text-left">{{strength}} (+{{strengthGear}})</div>
      <div class="points col-md-1 text-left">{{strengthPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <button v-on:click="changeStrength(true)">+</button>
        {{strengthCost()}}
        <button v-on:click="changeStrength(false)">-</button>
      </div>
    </div>

    <div class="row" id="agility">
      <div class="label col-md-6 text-left">Agility:</div>
      <div class="feats col-md-1 text-left">{{agility}} (+{{agilityGear}})</div>
      <div class="points col-md-1 text-left">{{agilityPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <button v-on:click="changeAgility(true)">+</button>
        {{agilityCost()}}
        <button v-on:click="changeAgility(false)">-</button>
      </div>
    </div>

    <div class="row" id="vitality">
      <div class="label col-md-6 text-left">Vitality:</div>
      <div class="feats col-md-1 text-left">{{vitality}} (+{{vitalityGear}})</div>
      <div class="points col-md-1 text-left">{{vitalityPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <button v-on:click="changeVitality(true)">+</button>
        {{vitalityCost()}}
        <button v-on:click="changeVitality(false)">-</button>
      </div>
    </div>

    <div class="row" id="accuracy">
      <div class="label col-md-6 text-left">Accuracy:</div>
      <div class="feats col-md-1 text-left">{{accuracy}} (+{{accuracyGear}})</div>
      <div class="points col-md-1 text-left">{{accuracyPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <button v-on:click="changeAccuracy(true)">+</button>
        {{accuracyCost()}}
        <button v-on:click="changeAccuracy(false)">-</button>
      </div>
    </div>

    <div class="row" id="grit">
      <div class="label col-md-6 text-left">Grit:</div>
      <div class="feats col-md-1 text-left">{{grit}} (+{{gritGear}})</div>
      <div class="points col-md-1 text-left">{{gritPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <button v-on:click="changeGrit(true)">+</button>
        {{gritCost()}}
        <button v-on:click="changeGrit(false)">-</button>
      </div>
    </div>

    <div class="row" id="encumberance">
      <div class="label col-md-6 text-left">Encumberance:</div>
      <div class="feats col-md-1 text-left">{{encumberance}} (+{{encumberanceGear}})</div>
      <div class="points col-md-1 text-left">{{encumberancePoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <button v-on:click="changeEncumberance(true)">+</button>
        {{encumberanceCost()}}
        <button v-on:click="changeEncumberance(false)">-</button>
      </div>
    </div>

    <div class="row" id="survival">
      <div class="label col-md-6 text-left">Survival:</div>
      <div class="feats col-md-1 text-left">{{survival}} (+{{survivalGear}})</div>
      <div class="points col-md-1 text-left">{{survivalPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <button v-on:click="changeSurvival(true)">+</button>
        {{survivalCost()}}
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
          <div class="col-md-4 text-left">From strength: {{strengthDamage()}} ({{strengthPercentage()}}%) </div>
          <div class="col-md-4 text-left">Total: {{strengthDamage() + 40}}</div>
        </div>

        <div class="row ranged">
          <div class="col-md-4 text-left">Base ranged damage: 40</div>
          <div class="col-md-4 text-left">From accuracy: {{accuracyDamage()}} ({{accuracyPercentage()}}%) </div>
          <div class="col-md-4 text-left">Total: {{accuracyDamage() + 40}}</div>
        </div>

        <div class="row armor">
          <div class="col-md-4 text-left">From agility: {{(agility + Number(agilityGear)) * 2}}</div>
          <div class="col-md-4 text-left">Damage Reduction: {{((agility + Number(agilityGear)) * 2) * 0.28}}%</div>
          <div class="col-md-4 text-left">Total: {{(agility + Number(agilityGear)) * 2}}</div>
        </div>

        <div class="row health">
          <div class="col-md-4 text-left">Base health: 200</div>
          <div class="col-md-4 text-left">From vitality: {{(vitality + Number(vitalityGear)) * 8}}</div>
          <div class="col-md-4 text-left">Total: {{(vitality + Number(vitalityGear)) * 8 + 200}}</div>
        </div>

        <div class="row stamina">
          <div class="col-md-4 text-left">Base stamina: 100</div>
          <div class="col-md-4 text-left">From grit: {{(grit + Number(gritGear)) * 3}} </div>
          <div class="col-md-4 text-left">Total: {{(grit + Number(gritGear)) * 3 + 100}}</div>
        </div>

        <div class="row encumberance">
          <div class="col-md-4 text-left">Base encumberance: 70</div>
          <div class="col-md-4 text-left">From encumberance: {{(encumberance + Number(encumberanceGear)) * 7}}</div>
          <div class="col-md-4 text-left">Total: {{(encumberance + Number(encumberanceGear)) * 7 + 70}}</div>
        </div>

      </div>

      <div class="col-md-5">
        <div class="row">
          <div class="col-12 text-right"><p>Feats from gear, elixir, warpaint etc.</p></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Strength: <input type="number" v-model="strengthGear" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Agility: <input type="number" v-model="agilityGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Vitality: <input type="number" v-model="vitalityGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Accuracy: <input type="number" v-model="accuracyGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Grit: <input type="number" v-model="gritGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Encumberance: <input type="number" v-model="encumberanceGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Survival: <input type="number" v-model="survivalGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><button v-on:click="resetGear()">Reset</button></div>
        </div>

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
      strengthGear: 0,

      agility: 0,
      agilityPoints: 0,
      agilityGear: 0,

      vitality: 0,
      vitalityPoints: 0,
      vitalityGear: 0,

      accuracy: 0,
      accuracyPoints: 0,
      accuracyGear: 0,

      grit: 0,
      gritPoints: 0,
      gritGear: 0,

      encumberance: 0,
      encumberancePoints: 0,
      encumberanceGear: 0,

      survival: 0,
      survivalPoints: 0,
      survivalGear: 0,

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

    pointCalculation: function(increment, current, gear) {
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
      for (var i = gear; i < newFeat; i++) {
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
      var newValues = this.pointCalculation(increment, this.strength, Number(this.strengthGear));
      this.strength = newValues.feat;
      this.points = newValues.points;
      this.strengthPoints = newValues.spentPoints;
    },

    strengthDamage() {
      return 40 * (((this.strength + Number(this.strengthGear)) * 2) / 100);
    },

    strengthPercentage() {
      return (this.strength + Number(this.strengthGear)) * 2;
    },

    changeAgility: function(increment) {
      var newValues = this.pointCalculation(increment, this.agility, Number(this.agilityGear));
      this.agility = newValues.feat;
      this.points = newValues.points;
      this.agilityPoints = newValues.spentPoints;
    },

    changeVitality: function(increment) {
      var newValues = this.pointCalculation(increment, this.vitality, Number(this.vitalityGear));
      this.vitality = newValues.feat;
      this.points = newValues.points;
      this.vitalityPoints = newValues.spentPoints;
    },

    changeAccuracy: function(increment) {
      var newValues = this.pointCalculation(increment, this.accuracy, Number(this.agilityGear));
      this.accuracy = newValues.feat;
      this.points = newValues.points;
      this.accuracyPoints = newValues.spentPoints;
    },

    accuracyDamage() {
      return 40 * (((this.accuracy + Number(this.accuracyGear)) * 2) / 100);
    },

    accuracyPercentage() {
      return (this.accuracy + Number(this.accuracyGear)) * 2;
    },

    changeGrit: function(increment) {
      var newValues = this.pointCalculation(increment, this.grit, Number(this.gritGear));
      this.grit = newValues.feat;
      this.points = newValues.points;
      this.gritPoints = newValues.spentPoints;
    },

    changeEncumberance: function(increment) {
      var newValues = this.pointCalculation(increment, this.encumberance, Number(this.encumberanceGear));
      this.encumberance = newValues.feat;
      this.points = newValues.points;
      this.encumberancePoints = newValues.spentPoints;
    },

    changeSurvival: function(increment) {
      var newValues = this.pointCalculation(increment, this.survival, Number(this.survivalGear));
      this.survival = newValues.feat;
      this.points = newValues.points;
      this.survivalPoints = newValues.spentPoints;
    },

    strengthCost() {
      return (this.strength - this.strength % 5) / 5 + 1;
    },

    agilityCost() {
      return (this.agility - this.agility % 5) / 5 + 1;
    },

    vitalityCost() {
      return (this.vitality - this.vitality % 5) / 5 + 1;
    },

    accuracyCost() {
      return (this.accuracy - this.accuracy % 5) / 5 + 1;
    },

    gritCost() {
      return (this.grit - this.grit % 5) / 5 + 1;
    },

    encumberanceCost() {
      return (this.encumberance - this.encumberance % 5) / 5 + 1;
    },

    survivalCost() {
      return (this.survival - this.survival % 5) / 5 + 1;
    },

    resetGear() {
      this.strengthGear = 0;
      this.agilityGear = 0;
      this.vitalityGear = 0;
      this.accuracyGear = 0;
      this.gritGear = 0;
      this.encumberanceGear = 0;
      this.survivalGear = 0;
    },
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
