<template>
  <v-app>
    <v-main>
    <div class="d-flex app-container">
      <v-tabs
        v-model="selectedTab"
        direction="vertical"
        bg-color="primary"
      >
        <v-tab v-for="(team, index) in teams" :value="team.owner" :key="team.name" :class="{'division-divider': index === 3 || index === 7}">
          <v-img contain height="30" width="30" :src="team.logo"></v-img>
          <span class="team-name">{{ team.name }}</span>
        </v-tab>
        <div class="d-flex justify-center mt-16">
          <v-btn width="100px" color="error" @click="clearClicked">Clear</v-btn>
        </div>
      </v-tabs>
      <v-window>
        <v-window-item v-for="team in teams" :key="team.owner" :value="selectedTab">
          <div class="d-flex flex-column align-center">
          <v-img contain height="200" width="200" class="mt-4" :src="selectedTeam.logo"></v-img>
          <p>{{ selectedTeam.owner }}</p>
          <div class="mt-6 calculations">
              <v-card elevation="15" outlined class="pa-4">
                <p class="mb-2">Starting Salary Cap = {{ formatPrice(selectedTeam.startingSalaryCap) }}</p>
                <p class="mb-2">Total Player Salary = {{ formatPrice(getTotalPlayerSalary(selectedTeam.players)) }}</p>
                <p class="mb-2">Salary Cap Remaining = <span :class="{'red--text': getSalaryCapRemaining(selectedTeam) < 0}">{{ formatPrice(getSalaryCapRemaining(selectedTeam)) }}</span></p>
                <p class="mb-2">100% Tax = {{ formatPrice(get100Tax(selectedTeam)) }}</p>
                <p class="mb-1">200% Tax = {{ formatPrice(get200Tax(selectedTeam)) }}</p>
                <p class="grand-total pt-1">GRAND TOTAL = {{ formatPrice(getGrandTotal(selectedTeam)) }}</p>
              </v-card>
            </div>
            </div>
        </v-window-item>
      </v-window>
    </div>
    </v-main>
  </v-app>
</template>

<script>
import JpgBrownbombers from '@/assets/brownbombers.jpg';
import JpgPilots from '@/assets/pilots.jpg';
import JpgColt45s from '@/assets/colt45s.jpg';
import JpgBlackcrackers from '@/assets/blackcrackers.jpg';
import JpgSenators from '@/assets/senators.jpg';
import JpgBraves from '@/assets/braves.jpg';
import JpgGiants from '@/assets/giants.jpg';
import JpgExpos from '@/assets/expos.jpg';
import JpgAngels from '@/assets/angels.jpg';
import JpgTerriers from '@/assets/terriers.jpg';
import JpgStars from '@/assets/stars.jpg';
import JpgDodgers from '@/assets/dodgers.jpg';

  export default {
    data() {
    return {
      selectedTab: null,

      teams: [{
        logo: JpgBrownbombers,
        name: 'Chicago Brownbombers',
        owner: 'Gabe',
        players: [],
        startingSalaryCap: 500,
      }, {
        logo: JpgPilots,
        name: 'Seattle Pilots',
        owner: 'Jay',
        players: [],
        startingSalaryCap: 865,
      }, {
        logo: JpgColt45s,
        name: 'Houston Colt .45s',
        owner: 'Adam',
        players: [],
        startingSalaryCap: 500,
      },{
        logo: JpgBlackcrackers,
        name: 'Atlanta BlackCrackers',
        owner: 'Bill',
        players: [],
        startingSalaryCap: 137,
      }, {
        logo: JpgSenators,
        name: 'Washington Senators',
        owner: 'Justin',
        players: [],
        startingSalaryCap: 753,
      },   {
        logo: JpgBraves,
        name: 'Boston Braves',
        owner: 'Dave/Tyler',
        players: [],
        startingSalaryCap: 62,
      }, {
        logo: JpgGiants,
        name: 'Zulu Cannibal Giants',
        owner: 'Bob',
        players: [],
        startingSalaryCap: 802,
      },{
        logo: JpgExpos,
        name: 'Montreal Expos',
        owner: 'Tom',
        players: [],
        startingSalaryCap: 500,
      },{
        logo: JpgAngels,
        name: 'California Angels',
        owner: 'Victor',
        players: [],
        startingSalaryCap: 500,
      }, {
        logo: JpgTerriers,
        name: 'St. Louis Terriers',
        owner: 'Chet',
        players: [],
        startingSalaryCap: 475,
      },   {
        logo: JpgStars,
        name: 'Detroit Stars',
        owner: 'Chris',
        players: [],
        startingSalaryCap: 708,
      }, {
        logo: JpgDodgers,
        name: 'Brooklyn Dodgers',
        owner: 'Erik',
        players: [],
        startingSalaryCap: 198,
      }],
    };
  },

  computed: {
    selectedTeam(){
      return this.teams.find((team)=>team.owner === this.selectedTab)
    }
  },
  methods: {
    clearClicked(){

    },
  formatPrice(value) {
      const formatter = new Intl.NumberFormat('en-US', {
        currency: 'USD',
        minimumFractionDigits: 0,
        style: 'currency',
      });
      return formatter.format(value);
    },
    get100Tax(team) {
      if (this.getSalaryCapRemaining(team) < 0) {
        const taxableAmount = this.getTotalPlayerSalary(team.players) - team.startingSalaryCap;
        return taxableAmount > 100 ? 100 : taxableAmount;
      }
      return 0;
    },
    get200Tax(team) {
      if (this.getSalaryCapRemaining(team) < -100) {
        let taxableAmount = this.getTotalPlayerSalary(team.players) - team.startingSalaryCap;
        taxableAmount -= 100;
        return taxableAmount * 2;
      }
      return 0;
    },
    getGrandTotal(team) {
      return this.getTotalPlayerSalary(team.players) + this.get100Tax(team) + this.get200Tax(team);
    },
    getLogo(logo){
      return `@/assets/${logo}.jpg`;
    },
    getSalaryCapRemaining(team) {
      return team.startingSalaryCap - this.getTotalPlayerSalary(team.players);
    },
    getTotalPlayerSalary(players) {
      return players.map((player) => parseInt(player.salary, 10)).reduce((prev, curr) => prev + curr, 0);
    },
  },
  }
</script>

<style scoped>
.app-container {
  height: 100vh;
}

p {
  font-size: 28px;
}

.calculations {
  text-align: right;
}

.division-divider {
  border-bottom: 1px solid white;
}

.grand-total {
  border-top: 3px solid black;
}

.team-name {
  margin-left: 8px;
  min-width: 205px;
  text-align: left;
}
</style>
