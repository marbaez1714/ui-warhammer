<template>
  <div class="container">
    <div>
      <h1 class="title">ui-warhammer</h1>
      <!-- Key Row -->
      <div class="key-row">
        <!-- Key -->
        <div class="table-wrapper">
          <table class="key-table">
            <thead>
              <tr class="table-title">
                <th colspan="4">Key</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <th>M</th>
                <td>Models</td>
                <th>WS</th>
                <td>Weapon Skill</td>
              </tr>
              <tr>
                <th>BS</th>
                <td>Ballistic Skill</td>
                <th>S</th>
                <td>Strength</td>
              </tr>
              <tr>
                <th>A</th>
                <td>Melee Attacks</td>
                <th>R</th>
                <td>Range</td>
              </tr>
              <tr>
                <th>T</th>
                <td>Toughness</td>
                <th>Ns</th>
                <td>Number of Shots</td>
              </tr>
              <tr>
                <th>AP</th>
                <td>Armour Penetration</td>
                <th>D</th>
                <td>Damage</td>
              </tr>
              <tr>
                <th>W</th>
                <td>Wounds</td>
                <th>AS</th>
                <td>Armor Save</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- Input Row - Attacker -->
      <div class="row">
        <!-- Attacker -->
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="5">Attacker</th>
              </tr>
              <tr class="table-headers">
                <th>M</th>
                <th>WS</th>
                <th>BS</th>
                <th>S</th>
                <th>A</th>
              </tr>
            </thead>
            <tbody>
              <tr class="stat-inputs">
                <td>
                  <input v-model="attacker.models" />
                </td>
                <td>
                  <input v-model="attacker.weaponSkill" />
                </td>
                <td>
                  <input v-model="attacker.ballistic" />
                </td>
                <td>
                  <input v-model="attacker.strength" />
                </td>
                <td>
                  <input v-model="attacker.attacks" />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="4">Defender</th>
              </tr>
              <tr class="table-headers">
                <th>M</th>
                <th>T</th>
                <th>AS</th>
                <th>W</th>
              </tr>
            </thead>
            <tbody>
              <tr class="stat-inputs">
                <td>
                  <input v-model="defender.models" />
                </td>
                <td>
                  <input v-model="defender.toughness" />
                </td>
                <td>
                  <input v-model="defender.armorSave" />
                </td>
                <td>
                  <input v-model="defender.wounds" />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <!-- Weapon -->
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="6">Weapon</th>
              </tr>
              <tr class="table-headers">
                <th>Name</th>
                <th>Ns</th>
                <th>R</th>
                <th>S</th>
                <th>AP</th>
                <th>D</th>
              </tr>
            </thead>
            <tbody>
              <tr class="stat-inputs">
                <td>
                  <select v-model="weapon">
                    <option :value="weapon" default disabled>{{weapon.name}}</option>
                    <option
                      v-for="(weapon,idx) in allWeapons"
                      :value="weapon"
                      :key="weapon.name+idx"
                    >{{weapon.name}}</option>
                  </select>
                </td>
                <td>
                  <input v-model="weapon.numberShots" />
                </td>
                <td>
                  <input v-model="weapon.range" />
                </td>
                <td>
                  <input v-model="weapon.strength" />
                </td>
                <td>
                  <input v-model="weapon.armorP" />
                </td>
                <td>
                  <input v-model="weapon.damage" />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- Input Row - Defender -->
      <div class="row">
        <!-- Defender -->
      </div>
      <!-- Results Row -->
      <div class="row">
        <!-- To Roll -->
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="4">Rolls Needed</th>
              </tr>
              <tr class="table-headers">
                <th>To</th>
                <th>Hit</th>
                <th>Wound</th>
                <th>Save</th>
              </tr>
            </thead>
            <tbody>
              <tr class="results">
                <td></td>
                <td>{{attacker.weaponSkill}}+</td>
                <td>{{results.woundRoll}}+</td>
                <td>{{results.armorSave}}+</td>
              </tr>
            </tbody>
          </table>
        </div>
        <!-- Odds -->
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="4">Chance Percentages</th>
              </tr>
              <tr class="table-headers">
                <th>To</th>
                <th>Hit</th>
                <th>Wound</th>
                <th>Save</th>
              </tr>
            </thead>
            <tbody>
              <tr class="results">
                <td></td>
                <td>{{Math.round(results.toHitOdds*100)}} %</td>
                <td>{{Math.round(results.woundOdds*100)}} %</td>
                <td>{{Math.round(results.armorSaveOdds*100)}} %</td>
              </tr>
            </tbody>
          </table>
        </div>
        <!-- Damage -->
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="2">Potential</th>
              </tr>
              <tr class="table-headers">
                <th>Wounds</th>
                <th>Damage</th>
              </tr>
            </thead>
            <tbody>
              <tr class="results">
                <td>{{Math.round(results.numberOfSuccessfulWounds)}}</td>
                <td>{{ Math.round(results.numberOfSuccessfulWounds * weapon.damage)}}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- Damage Table Row -->
      <div class="row"></div>
      <button @click="onShoot" class="shoot">Shoot</button>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import axios from "axios";

export default {
  components: {
    Logo
  },
  data() {
    return {
      attacker: {
        models: 1,
        weaponSkill: 3,
        ballistic: 3,
        strength: 4,
        attacks: 2
      },
      weapon: {
        name: "Select Weapon",
        type: "",
        range: 0,
        numberShots: 0,
        armorP: 0,
        damage: 0
      },
      defender: {
        models: 1,
        toughness: 3,
        armorSave: 5,
        wounds: 1
      },
      results: {
        toHitOdds: 0,
        woundRoll: 6,
        woundOdds: 0,
        armorSave: 6,
        armorSaveOdds: 0,
        numberOfSuccessfulWounds: 0
      },
      allWeapons: null
    };
  },
  mounted() {
    axios.get("http://localhost:5000/api/weapons").then(response => {
      this.allWeapons = response.data.weapons;
    });
  },
  methods: {
    onShoot() {
      const stats = {
        strength: this.weapon.strength,
        toughness: this.defender.toughness
      };
      axios
        .post("http://localhost:5000/api/wound", {
          strength: this.weapon.strength,
          armorP: this.weapon.armorP,
          toughness: this.defender.toughness,
          save: this.defender.armorSave,
          weaponSkill: this.attacker.weaponSkill,
          totalShots:
            parseInt(this.weapon.numberShots) * parseInt(this.attacker.models)
        })
        .then(response => {
          this.results = response.data.results;
        });
    }
  }
};
</script>

<style lang="scss">
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background: #e4e4e3;
  background-image: url("../assets/bedge-grunge.png");
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.row {
  display: flex;
  justify-content: center;
}

.table-wrapper {
  border-radius: 8px;
  display: inline-block;
  overflow: hidden;
  border: 2px solid black;
  margin: 10px;
  height: 100%;
}
.key-table {
  border-collapse: collapse;
  .table-title {
    th {
      background: #393a44;
      color: white;
      font-size: 16px;
      padding: 8px;
    }
  }
  tbody {
    th {
      background: #aeafa9;
      color: #13141a;
      padding: 8px;
    }
    td {
      padding-left: 8px;
      padding-right: 8px;
      background: white;
    }
  }
}
.stat-table {
  border-collapse: collapse;
  border: none;
  text-align: center;
  .table-title {
    th {
      background: #393a44;
      color: white;
      font-size: 16px;
      padding: 8px;
    }
  }
  .table-headers {
    background: #aeafa9;
    color: #13141a;
    th {
      padding: 8px;
    }
  }
  .stat-inputs {
    background: white;
    input {
      background: none;
      border: none;
      text-align: center;
      font-size: 16px;
      width: 48px;
      padding: 8px;
    }
    select {
      border: none;
      background: none;
      font-size: 16px;
    }
  }
  .results {
    td {
      background: white;
      height: 18px;
      padding: 9px;
    }
  }
  .shoot{
    font-size: 20px;
  }
}
</style>
