<template>
  <v-app>
    <v-main>
      <v-card width="1000" class="mx-auto mt-5">
        <v-card-title>
          <h2 class="display1">Starship Generator</h2>
        </v-card-title>
        <v-divider></v-divider>
        <v-card-text>
          <p id="ship-name"><strong>Name:</strong> {{shipPrefix}} {{shipName}}</p>
          <p id="ship-class"><strong>Class:</strong> {{shipClass}}</p>
          <v-col>
              <v-card width="900" class="mt-5">
                <v-card-title>
                  <h3 class="display1">Safety Info</h3>
                </v-card-title>
                <v-card-text>
                  <p><strong>Max Passengers:</strong> {{safety.maxPassengers}}</p>
                  <p><strong>Lifepods:</strong> {{safety.lifepods.amount}}, each holding {{safety.lifepods.passengers}} passengers</p>
                </v-card-text>
              </v-card>          
              <v-card width="900" class="mt-5">
                <v-card-title>
                  <h3 class="display1">Combat Info</h3>
                </v-card-title>
                <v-card-text>
                  <p><strong>Primary Weapon:</strong> {{combat.weapons.main}}</p>
                  <p><strong>Secondary Weapon:</strong> {{combat.weapons.backup}}</p>
                </v-card-text>
              </v-card>  
          </v-col>
          
          <v-btn @click="generate" color="info"><v-icon>mdi-backup-restore</v-icon> Generate</v-btn><br>

          <p>Starship Generator by <a href="https://acei.us">AceiusIO</a></p>
        </v-card-text>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  data: () => ({
    possible: {
      prefixes: ['I.O.', 'I.M.S.', 'I.C.S.', 'L.C.S.', 'A.T.S.'],
      mainName: ['Argun', 'Wings', 'Firebolt', 'Solaris', 'Itzka', 'Dominator', 'Hive'],
      title: ['The ', 'B1 ', 'RF ', '', 'Shimmering ', 'Online ', 'Synergized ', 'Standstill ', 'Empowered ', 'LOC-1 ', 'Doomed ', 'BSD ', 'IPS ', 'Starworthy'],
      class: ['Capital Ship', 'Freighter', 'Frigate', 'Shuttle']
    },
    shipPrefix: 'I.O.',
    shipName: 'Katzuka',
    shipClass: 'Freighter',
    safety: {
      maxPassengers: 100,
      lifepods: {
        passengers: 6,
        amount: 20
      }
    },
    combat: {
      weapons: {
        possibleMain: ['Battery Turrets', 'Missle Launcher', 'Attack Redirection Drones'],
        possibleBackup: ['Phasers', 'Turrets' , 'Jump Disentanglement Field'],
        main: 'Battery Turrets',
        backup: 'Phasers'
      }
    }
  }),

  methods: {
    generate: function(){
      console.clear();

      //// Generate General Info

      this.shipPrefix = this.possible.prefixes[Math.floor(Math.random() * this.possible.prefixes.length)]
      this.shipName = this.possible.title[Math.floor(Math.random() * this.possible.title.length)] + this.possible.mainName[Math.floor(Math.random() * this.possible.mainName.length)]
      this.shipClass = this.possible.class[Math.floor(Math.random() * this.possible.class.length)]

      //// Generate Safety Info

      // Generate Max Passengers

      if (this.shipClass == 'Capital Ship') {
        this.safety.maxPassengers = Math.floor((Math.random() * 350) + 1);
      } else if (this.shipClass == 'Freighter') {
        this.safety.maxPassengers = Math.floor((Math.random() * 200) + 1);
      } else if (this.shipClass == 'Frigate') {
        this.safety.maxPassengers = Math.floor((Math.random() * 75) + 1);
      } else if (this.shipClass == 'Shuttle') {
        this.safety.maxPassengers = Math.floor((Math.random() * 50) + 1);
      }

      // Generate Max Capacity of Lifepods

      this.safety.lifepods.passengers = Math.floor((Math.random() * 6) + 1);

      // Dertimine Amount of Lifepods factoring Max Capacity

      this.safety.lifepods.amount = Math.round(this.safety.maxPassengers / this.safety.lifepods.passengers) + 1

      //// Generate Combat Info

      // Select Primary Weapon

      this.combat.weapons.main = this.combat.weapons.possibleMain[Math.floor(Math.random() * this.combat.weapons.possibleMain.length)]

      // Select Backup Weapon

      this.combat.weapons.backup = this.combat.weapons.possibleBackup[Math.floor(Math.random() * this.combat.weapons.possibleBackup.length)]
    }
  }
};
</script>