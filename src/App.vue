<template>
  <div>
    <RDSInput @lookup-pi="convertPi" />
  </div>
  <div class="light-textarea tight-padding">
    <p>Results for PI Code: {{ piCode }}</p>
  </div>
  <div class="light-textarea" :key=record.id v-for="record in rdsRecords">
    <li>Match Type: {{ this.rdsMethodMessage }}</li>
    <li>Callsign: {{ record.callsign }}</li>
    <li>Frequency: {{ record.frequency }}</li>
    <li>Location: {{ record.city }}, {{ record.sp }}, {{ record.country }}</li>
  </div>
</template>

<script>
import RDSInput from './components/RDSInput.vue'

export default {
  name: 'App',
  components: {
    RDSInput
  },
  methods: {
    async convertPi(piCode) {
      const res = await fetch(`https://dev-api.fmlogger.com/rdssearch/${piCode}`)
      const data = await res.json()
      this.piCode = piCode
      this.rdsRecords = data.records
      this.rdsRecordCount = data.record_count
      this.rdsMethod = data.rds_method
    }
  },
  data () {
    return {
      piCode: '',
      rdsRecords: '',
      rdsRecordCount: '',
      rdsMethod: '',
    }
  },
  computed: {
    rdsMethodMessage() {
      let msg = ''
      if (this.rdsMethod === 'db_match') {
        msg = 'WTFDA DB Match'
      } else if (this.rdsMethod === 'pi_decode') {
        msg = 'PI Code (not in DB)'
      }
      return msg
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@600&display=swap');

body {
  font-family: 'Montserrat', sans-serif; 
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  font-size: 1.2rem;
  background-color:#6B7280;
}

.light-textarea {
  padding: 3px 7px;
  border-radius: 5px;
  max-width: 100%;
  list-style-type: none;
  background-color: #DBDBDB;
  margin: 5px;
  box-shadow: 0 3px 1px -2px rgb(0 0 0 / 16%), 0 2px 2px 0 rgb(0 0 0 / 11%), 0 1px 5px 0 rgb(0 0 0 / 10%);
}

.tight-padding {
  padding: 1px 5px;
}
</style>