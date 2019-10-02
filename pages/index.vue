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
        <!-- Weapon -->
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="5">Weapon</th>
              </tr>
              <tr class="table-headers">
                <th>Name</th>
                <th>Ns</th>
                <th>R</th>
                <th>AP</th>
                <th>D</th>
              </tr>
            </thead>
            <tbody>
              <tr class="stat-inputs">
                <td>
                  <input v-model="weapon.name" />
                </td>
                <td>
                  <input v-model="weapon.numberShots" />
                </td>
                <td>
                  <input v-model="weapon.range" />
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
                <td>1</td>
                <td>1</td>
                <td>1</td>
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
                <td>1</td>
                <td>1</td>
                <td>1</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- Damage Table Row -->
      <div class="row">
        <!-- Damage -->
        <div class="table-wrapper">
          <table class="stat-table">
            <thead>
              <tr class="table-title">
                <th colspan="4">Chance Percentages</th>
              </tr>
              <tr class="table-headers">
                <th>Damage</th>
                <th>Chance</th>
              </tr>
            </thead>
            <tbody>
              <tr
                class="results"
                v-for="(shots, index) in parseInt(weapon.numberShots) * parseInt(attacker.models)||1"
                :key="index+'damage'"
              >
                <td>{{ shots * weapon.damage}}</td>
                <td>1</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  components: {
    Logo
  },
  data() {
    return {
      attacker: {
        models: 1,
        weaponSkill: 2,
        ballistic: 2,
        strength: 2,
        attacks: 2
      },
      weapon: {
        name: "",
        numberShots: 10,
        range: 1,
        armorP: 1,
        damage: 1
      },
      defender: {
        models: 1,
        toughness: 1,
        armorSave: 1,
        wounds: 1
      }
    };
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
  }
  .results {
    td {
      background: white;
      height: 18px;
      padding: 9px;
    }
  }
}
</style>
