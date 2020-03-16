<template>
  <q-page class="flex flex-center">
    <q-card class="my-card">
      <q-card-section>
        <div class="text-h6"><center>Parken in Erfurt</center></div>
      </q-card-section>
      <q-separator inset />
      <q-card-section>
        <div>
          <center>
            <q-icon name="face" /><br />
            Alexander Gr&uuml;&szlig;ung
            <br /><br />
            <q-icon name="info" /><br />
            Version 3.0
            <br /><br />
            <q-icon name="favorite" /><br />
            Vielen Dank an die Stadt Erfurt für die Bereitstellung der Daten.<br/>www.geoportal.erfurt.de
          </center>
        </div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'AboutIndex',

}
</script>
<style lang="sass" scoped>
  .my-card
    width: 100%
    max-width: 400px
</style>
