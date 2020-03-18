<template>
  <q-page class="">
    <q-pull-to-refresh @refresh="loadData">
      <q-card
        :class="parkhaus.cssClass"
        :key="parkhaus.id"
        bordered
        clickable
        style="margin: 20px;"
        v-for="(parkhaus, i) in parkhausData">
        <div v-ripple @click="showCard(i)" class="cursor-pointer relative-position">
          <q-card-section>
            <div class="text-h6">{{ parkhaus.name }}
              <q-icon :name="parkhaus.tendenzImage"></q-icon>

            </div>
          </q-card-section>
        </div>
      </q-card>

      <div style="opacity: 0.5" class="fixed-center" v-if="(error && parkhausData.length <= 0)">
        <div class="text-h5 text-primary text-center">
          <q-icon
            name="wifi_off"
            size="100px"
            color="primary"
            /> <br />
          Es besteht keine Verbindung zum Internet.
        </div>
      </div>

    </q-pull-to-refresh>

    <q-dialog v-model="openCard">
      <q-card>
        <q-card-section>
          <div class="text-h6">{{alertData.name}}</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          Plätze frei: {{alertData.frei}}<br/>
          Belegt: {{alertData.belegt}}/{{alertData.gesamt}}<br/>
          <br/>
          Tendenz: {{alertData.tendenz}}<br/>
          Status: {{alertData.oeffnungszustand}}
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup/>
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
  export default {
    name: 'PageIndex',

    openCard: false,
    alertData: [],


    methods: {
      loadData(done) {
        let self = this;
        this.$axios.get('https://api.gruessung.eu/parken/output.php')
          .then(function (result) {
            result.data.forEach((parkhaus, index) => {

              let iProzent = (100 * parkhaus.frei) / parkhaus.gesamt;

              if (iProzent >= 50) {
                result.data[index].cssClass = 'bg-green-1';
              } else if (iProzent < 50) {
                result.data[index].cssClass = 'bg-yellow-1';
              } else if (iProzent < 20) {
                result.data[index].cssClass = 'bg-red-1';
              }

              if (parkhaus.tendenz == 'steigend') {
                result.data[index].tendenzImage = 'trending_up';
              } else if (parkhaus.tendenz == 'gleichbleibend') {
                result.data[index].tendenzImage = 'trending_flat';
              } else if (parkhaus.tendenz == 'fallend') {
                result.data[index].tendenzImage = 'trending_down';
              }

            });
            self.parkhausData = result.data;
            self.error = false;
            done();
          })
          .catch(function (err) {
            console.log(err);
            self.error = true;
            done();
          })

      },

      showCard(index) {
        console.log(this.parkhausData[index]);
        this.alertData = this.parkhausData[index];
        this.openCard = true


      }
    },

    data() {
      this.loadData();
      return {
        leftDrawerOpen: false,
        parkhausData: [],
        error: false,
        openCard: false,
        alertData: []
      }
    },

  }
</script>
