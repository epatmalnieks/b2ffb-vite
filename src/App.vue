<template>
  <v-app>
    <v-main>
    <div class="d-flex flex-row">
      <v-tabs
        v-model="selectedTab"
        direction="vertical"
        color="primary"
      >
        <v-tab value="gabe">
          <v-icon start>
            mdi-account
          </v-icon>
          Chicago Brownbombers
        </v-tab>
        <v-tab value="jay">
          <v-icon start>
            mdi-lock
          </v-icon>
          Seattle Pilots
        </v-tab>
        <v-tab value="adam">
          <v-icon start>
            mdi-access-point
          </v-icon>
          Houston Colt .45s
        </v-tab>
        <v-tab value="bill">
          <v-icon start>
            mdi-access-point
          </v-icon>
          Atlanta Blackcrackers
        </v-tab>
        <v-tab value="justin">
          <v-icon start>
            mdi-account
          </v-icon>
          Washington Senators
        </v-tab>
        <v-tab value="dave">
          <v-icon start>
            mdi-lock
          </v-icon>
          Boston Braves
        </v-tab>
        <v-tab value="bob">
          <v-icon start>
            mdi-access-point
          </v-icon>
          Zulu Cannibal Giants
        </v-tab>
        <v-tab value="tom">
          <v-icon start>
            mdi-access-point
          </v-icon>
          Montreal Expos
        </v-tab>
        <v-tab value="victor">
          <v-icon start>
            mdi-account
          </v-icon>
          California Angels
        </v-tab>
        <v-tab value="chet">
          <v-icon start>
            mdi-lock
          </v-icon>
          St. Louis Terriers
        </v-tab>
        <v-tab value="chris">
          <v-icon start>
            mdi-access-point
          </v-icon>
          Detroit Stars
        </v-tab>
        <v-tab value="erik">
          <v-icon start>
            mdi-access-point
          </v-icon>
          Brooklyn Dodgers
        </v-tab>
      </v-tabs>
      <v-window v-model="selectedTab">
        <v-window-item value="erik">
          <v-card flat>
            <v-card-text>
              <p>
                Sed aliquam ultrices mauris. Donec posuere vulputate arcu. Morbi ac felis. Etiam feugiat lorem non metus. Sed a libero.
              </p>

              <p>
                Nam ipsum risus, rutrum vitae, vestibulum eu, molestie vel, lacus. Aenean tellus metus, bibendum sed, posuere ac, mattis non, nunc. Aliquam lobortis. Aliquam lobortis. Suspendisse non nisl sit amet velit hendrerit rutrum.
              </p>

              <p class="mb-0">
                Phasellus dolor. Fusce neque. Fusce fermentum odio nec arcu. Pellentesque libero tortor, tincidunt et, tincidunt eget, semper nec, quam. Phasellus blandit leo ut odio.
              </p>
            </v-card-text>
          </v-card>
        </v-window-item>
      </v-window>
    </div>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      selectedTab: null,
    }),
  }
</script>
