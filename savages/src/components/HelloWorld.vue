<template>
  <div class="container">
    <div class="row" id="points"><div class="col-12">Unspent Points: {{points}} <button v-on:click="resetPoints()">Reset Points</button></div></div>
    
    <div class="row headers">
      <div class="col-md-6 text-left"></div>
      <div class="col-md-1 text-left">Attributes</div>
      <div class="col-md-1 text-left">Points</div>
      <div class="col-md-4 text-left text-right">Cost</div>
    </div>

    <div class="row attribute" id="strength">
      <div class="label col-md-6 text-left">Strength:</div>
      <div class="attributes col-md-1 text-left">{{strength}} (+{{strengthGear}})</div>
      <div class="points col-md-1 text-left">{{strengthPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <div class="row">
          <div class="col-md-9"></div>
          <div class="col-md-1">
            <button v-on:click="changeStrength(false)">-</button>
          </div>
          <div class="col-md-1">
            {{strengthCost()}}
          </div>
          <div class="col-md-1">
            <button v-on:click="changeStrength(true)">+</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row attribute" id="agility">
      <div class="label col-md-6 text-left">Agility:</div>
      <div class="attributes col-md-1 text-left">{{agility}} (+{{agilityGear}})</div>
      <div class="points col-md-1 text-left">{{agilityPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <div class="row">
          <div class="col-md-9"></div>
          <div class="col-md-1">
            <button v-on:click="changeAgility(false)">-</button>
          </div>
          <div class="col-md-1">
            {{agilityCost()}}
          </div>
          <div class="col-md-1">
            <button v-on:click="changeAgility(true)">+</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row attribute" id="vitality">
      <div class="label col-md-6 text-left">Vitality:</div>
      <div class="attributes col-md-1 text-left">{{vitality}} (+{{vitalityGear}})</div>
      <div class="points col-md-1 text-left">{{vitalityPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <div class="row">
          <div class="col-md-9"></div>
          <div class="col-md-1">
            <button v-on:click="changeVitality(false)">-</button>
          </div>
          <div class="col-md-1">
            {{vitalityCost()}}
          </div>
          <div class="col-md-1">
            <button v-on:click="changeVitality(true)">+</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row attribute" id="accuracy">
      <div class="label col-md-6 text-left">Accuracy:</div>
      <div class="attributes col-md-1 text-left">{{accuracy}} (+{{accuracyGear}})</div>
      <div class="points col-md-1 text-left">{{accuracyPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <div class="row">
          <div class="col-md-9"></div>
          <div class="col-md-1">
            <button v-on:click="changeAccuracy(false)">-</button>
          </div>
          <div class="col-md-1">
            {{accuracyCost()}}
          </div>
          <div class="col-md-1">
            <button v-on:click="changeAccuracy(true)">+</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row attribute" id="grit">
      <div class="label col-md-6 text-left">Grit:</div>
      <div class="attributes col-md-1 text-left">{{grit}} (+{{gritGear}})</div>
      <div class="points col-md-1 text-left">{{gritPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <div class="row">
          <div class="col-md-9"></div>
          <div class="col-md-1">
            <button v-on:click="changeGrit(false)">-</button>
          </div>
          <div class="col-md-1">
            {{gritCost()}}
          </div>
          <div class="col-md-1">
            <button v-on:click="changeGrit(true)">+</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row attribute" id="encumbrance">
      <div class="label col-md-6 text-left">Encumbrance:</div>
      <div class="attributes col-md-1 text-left">{{encumbrance}} (+{{encumbranceGear}})</div>
      <div class="points col-md-1 text-left">{{encumbrancePoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <div class="row">
          <div class="col-md-9"></div>
          <div class="col-md-1">
            <button v-on:click="changeEncumbrance(false)">-</button>
          </div>
          <div class="col-md-1">
            {{encumbranceCost()}}
          </div>
          <div class="col-md-1">
            <button v-on:click="changeEncumbrance(true)">+</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row attribute" id="survival">
      <div class="label col-md-6 text-left">Survival:</div>
      <div class="attributes col-md-1 text-left">{{survival}} (+{{survivalGear}})</div>
      <div class="points col-md-1 text-left">{{survivalPoints}}</div>
      <div class="point-buttons col-md-4 text-right">
        <div class="row">
          <div class="col-md-9"></div>
          <div class="col-md-1">
            <button v-on:click="changeSurvival(false)">-</button>
          </div>
          <div class="col-md-1">
            {{survivalCost()}}
          </div>
          <div class="col-md-1">
            <button v-on:click="changeSurvival(true)">+</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row stats">
      <div class="col-md-8">
        <div class="row">
          <div class="col-12"><p>Computed stats</p></div>
        </div>
        <div class="row base-stat meele">
          <div class="col-md-12">
            <div class="row">
              <div class="col-md-3 text-left">Weapon damage</div>
              <div class="col-md-3 text-left">From strength</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">Total</div>
            </div>

            <div class="row">
              <div class="col-md-3 text-left"><input class="base-input" type="number" v-model="baseMelee" min="0"></div>
              <div class="col-md-3 text-left">{{strengthDamage()}} ({{strengthPercentage()}}%) </div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">{{strengthDamage() + Number(baseMelee)}}</div>
            </div>
          </div>
        </div>


        <div class="row base-stat ranged">
          <div class="col-md-12">
            <div class="row">
              <div class="col-md-3 text-left">Bow + ammo damage</div>
              <div class="col-md-3 text-left">From accuracy</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">Total</div>
            </div>
            <div class="row">
              <div class="col-md-3 text-left"><input class="base-input" type="number" v-model="baseRanged" min="0"></div>
              <div class="col-md-3 text-left">{{accuracyDamage()}} ({{accuracyPercentage()}}%)</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">{{accuracyDamage() + Number(baseRanged)}}</div>
            </div>
          </div>
        </div>

        
        <div class="row base-stat armor">
          <div class="col-md-12">
            <div class="row">
              <div class="col-md-3 text-left">Gear armor</div>
              <div class="col-md-3 text-left">From agility</div>
              <div class="col-md-3 text-left">Damage Reduction</div>
              <div class="col-md-3 text-left">Total</div>
            </div>
            <div class="row">
              <div class="col-md-3 text-left"><input class="base-input" type="number" v-model="baseArmor" min="0"></div>
              <div class="col-md-3 text-left">{{(agility + Number(agilityGear)) * 2}}</div>
              <div class="col-md-3 text-left">{{Number((((agility + Number(agilityGear)) * 2) + Number(baseArmor)) * 0.28).toFixed(2)}}%</div>
              <div class="col-md-3 text-left">{{((agility + Number(agilityGear)) * 2) + Number(baseArmor)}}</div>
            </div>
          </div>
        </div>

        
        <div class="row base-stat health">
          <div class="col-md-12">
            <div class="row">
              <div class="col-md-3 text-left">Base health</div>
              <div class="col-md-3 text-left">From vitality</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">Total</div>
            </div>
            <div class="row">
              <div class="col-md-3 text-left"><input class="base-input" type="number" v-model="baseHealth" min="0"></div>
              <div class="col-md-3 text-left">{{(vitality + Number(vitalityGear)) * 8}}</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">{{(vitality + Number(vitalityGear)) * 8 + Number(baseHealth)}}</div>
            </div>
          </div>
        </div>


        <div class="row base-stat stamina">
          <div class="col-md-12">
            <div class="row">
              <div class="col-md-3 text-left">Base stamina</div>
              <div class="col-md-3 text-left">From grit</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">Total</div>
            </div>
            <div class="row">
              <div class="col-md-3 text-left"><input class="base-input" type="number" v-model="baseStamina" min="0"></div>
              <div class="col-md-3 text-left">{{(grit + Number(gritGear)) * 3}}</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">{{(grit + Number(gritGear)) * 3 + Number(baseStamina)}}</div>
            </div>
          </div>
        </div>

        <div class="row base-stat encumbrance">
          <div class="col-md-12">
            <div class="row">
              <div class="col-md-3 text-left">Base encumbrance</div>
              <div class="col-md-3 text-left">From encumbrance</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">Total</div>
            </div>
            <div class="row">
              <div class="col-md-3 text-left"><input class="base-input" type="number" v-model="baseEncumbrance" min="0"></div>
              <div class="col-md-3 text-left">{{(encumbrance + Number(encumbranceGear)) * 7}}</div>
              <div class="col-md-3 text-left"></div>
              <div class="col-md-3 text-left">{{(encumbrance + Number(encumbranceGear)) * 7 + Number(baseEncumbrance)}}</div>
            </div>
          </div>
        </div>

      </div>

      <div class="col-md-4">
        <div class="row">
          <div class="col-12 text-right"><p>Attributes from gear, elixir, warpaint etc.</p></div>
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
          <div class="col-12 text-right"><label>Encumbrance: <input type="number" v-model="encumbranceGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><label>Survival: <input type="number" v-model="survivalGear" placeholder="0" min="0"></label></div>
        </div>

        <div class="row">
          <div class="col-12 text-right"><button v-on:click="resetGear()">Reset</button></div>
        </div>

      </div>

    </div>

    <div class="row info">
      <div class="col-md-12">

        <div class="row strength-info">
          <div class="col-md-12 text-left">
            <h4>Strength</h4>
            <p>You gain 2% of your weapon damage as extra damage for every point in strength.</p>
          </div>
        </div>

        <div class="row agility-info">
          <div class="col-md-12 text-left">
            <h4>Agility</h4>
            <p>You gain +2 armor for every point in agility.  10 armor gives you 2.8% damage reduction.</p>
          </div>
        </div>

        <div class="row vitality-info">
          <div class="col-md-12 text-left">
            <h4>Vitality</h4>
            <p>You gain +8 health for every point in vitality.</p>
          </div>
        </div>

        <div class="row accuracy-info">
          <div class="col-md-12 text-left">
            <h4>Accuracy</h4>
            <p>You gain about 2% of your ranged damage (ammo damage + bow damage) as extra damage for each point in accuracy.<p>
            <p>If you know the exact damage calculation for accuracy, please open an issue on <a href="https://github.com/DownGoat/SAVAGES">GitHub</a> with the information.</p>
          </div>
        </div>

        <div class="row grit-info">
          <div class="col-md-12 text-left">
            <h4>Grit</h4>
            <p>You gain +3 stamina for every point in grit.</p>
          </div>
        </div>

        <div class="row grit-info">
          <div class="col-md-12 text-left">
            <h4>Encumbrance</h4>
            <p>You gain +7 encumbrance for every point in encumbrance.</p>
          </div>
        </div>

        <div class="row survival-info">
          <div class="col-md-12 text-left">
            <h4>Survival</h4>
            <p>Decreases the food/drink decay. If you know the exact calculation, please open an issue with information on <a href="https://github.com/DownGoat/SAVAGES">GitHub</a>.</p>
          </div>
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
      baseMelee: 40,
      baseRanged: 40,
      baseArmor: 100,
      baseHealth: 200,
      baseStamina: 100,
      baseEncumbrance: 70,

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

      encumbrance: 0,
      encumbrancePoints: 0,
      encumbranceGear: 0,

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
      this.encumbrance = 0;
      this.encumbrancePoints = 0;
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
        attribute: newFeat,
        cost: cost,
        spentPoints: spentPoints
      };
    },

    changeStrength: function(increment) {
      var newValues = this.pointCalculation(
        increment,
        this.strength,
        Number(this.strengthGear)
      );
      this.strength = newValues.attribute;
      this.points = newValues.points;
      this.strengthPoints = newValues.spentPoints;
    },

    strengthDamage() {
      return Number(
        Number(
          Number(this.baseMelee) *
            ((this.strength + Number(this.strengthGear)) * 2 / 100)
        ).toFixed(0)
      );
    },

    strengthPercentage() {
      return (this.strength + Number(this.strengthGear)) * 2;
    },

    changeAgility: function(increment) {
      var newValues = this.pointCalculation(
        increment,
        this.agility,
        Number(this.agilityGear)
      );
      this.agility = newValues.attribute;
      this.points = newValues.points;
      this.agilityPoints = newValues.spentPoints;
    },

    changeVitality: function(increment) {
      var newValues = this.pointCalculation(
        increment,
        this.vitality,
        Number(this.vitalityGear)
      );
      this.vitality = newValues.attribute;
      this.points = newValues.points;
      this.vitalityPoints = newValues.spentPoints;
    },

    changeAccuracy: function(increment) {
      var newValues = this.pointCalculation(
        increment,
        this.accuracy,
        Number(this.agilityGear)
      );
      this.accuracy = newValues.attribute;
      this.points = newValues.points;
      this.accuracyPoints = newValues.spentPoints;
    },

    accuracyDamage() {
      return Number(
        Number(
          Number(this.baseRanged) *
            ((this.accuracy + Number(this.accuracyGear)) * 2 / 100)
        ).toFixed(0)
      );
    },

    accuracyPercentage() {
      return (this.accuracy + Number(this.accuracyGear)) * 2;
    },

    changeGrit: function(increment) {
      var newValues = this.pointCalculation(
        increment,
        this.grit,
        Number(this.gritGear)
      );
      this.grit = newValues.attribute;
      this.points = newValues.points;
      this.gritPoints = newValues.spentPoints;
    },

    changeEncumbrance: function(increment) {
      var newValues = this.pointCalculation(
        increment,
        this.encumbrance,
        Number(this.encumbranceGear)
      );
      this.encumbrance = newValues.attribute;
      this.points = newValues.points;
      this.encumbrancePoints = newValues.spentPoints;
    },

    changeSurvival: function(increment) {
      var newValues = this.pointCalculation(
        increment,
        this.survival,
        Number(this.survivalGear)
      );
      this.survival = newValues.attribute;
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

    encumbranceCost() {
      return (this.encumbrance - this.encumbrance % 5) / 5 + 1;
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
      this.encumbranceGear = 0;
      this.survivalGear = 0;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h4 {
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

.base-input {
  width: 5em;
}

.attribute {
  margin-bottom: 1em;
}

.info {
  margin-top: 5em;
}

 .base-stat {
   margin-top: 2em;
 }
</style>
