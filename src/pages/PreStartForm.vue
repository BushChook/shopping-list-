<!-- eslint-disable vue/require-v-for-key -->
<template>
  <q-page class="flex flex-center">
    <div id="container">
      <h1>Zero Harm Pre-Start Meeting Record</h1>

      <q-form class="q-gutter-md">

        <!-- Section 1 -->
        <h2>Section 1- General Details</h2>
        <div class="form-section">
          <div class="row">
            <div class="col">
              <q-input filled v-model="preStartMeetingConductedBy" label="Pre-Start Meeting Conducted By"></q-input>
            </div>
          </div>

          <div class="row">
            <div class="col">
              <q-input filled v-model="jobNumber" label="Job Number"></q-input>
            </div>
            <div class="col">
              <q-input filled v-model="trafficRiskAssessmentNumber" label="Traffic Risk Assessment Number"></q-input>
            </div>
          </div>

          <div class="row">
            <div class="col">
              <q-input filled v-model="date" label="Date" type="date" stack-label></q-input>
            </div>
            <div class="col">
              <q-input filled v-model="time" label="Time" type="time" stack-label></q-input>
            </div>
            <div class="col">
              <q-checkbox v-model="emergencyEvacuationPointNominated" label="Emergency Evacuation Point Nominated"></q-checkbox>
            </div>
          </div>

          <div class="row">
            <div class="col">
              <q-input filled v-model="address" label="Address"></q-input>
            </div>
          </div>
        </div>

        <!-- Section 2 -->
        <h2>Section 2 - Permits/Notifications and Calibration/Test &amp; Tag</h2>
        <div class="form-section">
          <!-- Headings -->
          <div class="row">
            <div class="col">
              <div class="subheading text-center">Enter Permit Numbers</div>

              <!-- Permit Numbers -->
              <div class="row">
                <div v-for="(ignoreMe, permit) in permitNumbers" class="col-6">
                  <q-input filled v-model="permitNumbers[permit]" :label="permit"></q-input>
                </div>
              </div>
            </div>
            <div class="col">
              <div class="subheading text-center">Enter Calibration/Tag Dates</div>

              <!-- Tag Dates -->
              <div class="row">
                <div v-for="(ignoreMe, tagDate) in tagDates" class="col-6">
                  <q-input filled v-model="tagDates[tagDate]" :label="tagDate" type="date" stack-label :otion="tagDateExpiry" :bg-color="tagDateExpiry(tagDates[tagDate])"></q-input>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Section 4 -->
        <h2>Section 4 - Specific Requirements</h2>
        <div class="form-section">
          <div class="q-markup-table q-table__container q-table__card q-table--cell-separator q-table--flat q-table--bordered">
            <table class="q-table">
              <thead>
                <tr>
                  <th>Item</th>
                  <th>Site Specific Requirements</th>
                  <th>Yes/No/NA</th>
                  <th style="width:20%">If No/NA, why not?</th>
                  <th style="width:20%"></th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>1</td>
                  <td>A Current SWMS signed and understood by all personnel</td>
                  <td>
                    <q-radio v-model="swmsUnderstoodByAllPersonnel" val="Yes" label="Yes"></q-radio>
                    <q-radio v-model="swmsUnderstoodByAllPersonnel" val="No" label="No"></q-radio>
                    <q-radio v-model="swmsUnderstoodByAllPersonnel" val="NA" label="NA"></q-radio>
                  </td>
                  <td rowspan="2">
                    <q-input v-model="whyNot" filled type="textarea" input-style="min-height:35em;"></q-input>
                  </td>
                  <td rowspan="2">
                    <q-input v-model="whyNot" filled type="textarea" input-style="min-height:35em;"></q-input>
                  </td>
                </tr>
                <tr>
                  <td>2</td>
                  <td>Please tick the relevant SWMS applicable to undertake the job safely</td>
                  <td>
                    <div v-for="(ignore, swm) in swms">
                      <q-checkbox v-model="swms[swm]" :label="swm"></q-checkbox>
                    </div>
                  </td>
                </tr>
                <tr>
                  <td>3</td>
                  <td>Person assigned as Spotter</td>
                  <td colspan="3">
                    <q-input filled v-model="personAssignedAsSpotter" label="Person Assigned As Spotter"></q-input>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Section 5 -->
        <h2>Section 5 - Onsite Assessment of Underground Services</h2>

        <div class="row">
          <div v-for="(ignoreMe, undergroundService) in undergroundServices" class="col-4">
            <q-input filled v-model="undergroundServices[undergroundService]" :label="undergroundService" type="number" :bg-color="getAssetColor(undergroundServices[undergroundService])"></q-input>
          </div>
        </div>

        <div class="row">
          <div class="col-2">
            <p>Passive sweep with locator?</p>
          </div>
          <div class="col-2">
            <q-radio v-model="passiveSweepWithLocator" val="Yes" label="Yes"></q-radio>
            <q-radio v-model="passiveSweepWithLocator" val="No" label="No"></q-radio>
          </div>
          <div class="col-8">
            <q-input filled v-model="ifNoWhy1" label="If No Why?" type="text" ></q-input>
          </div>
        </div>

        <div class="row">
          <div class="col-2">
            <p>Assets within 500mm located?</p>
          </div>
          <div class="col-2">
            <q-radio v-model="assetsWithin500mmLocated" val="Yes" label="Yes"></q-radio>
            <q-radio v-model="assetsWithin500mmLocated" val="No" label="No"></q-radio>
          </div>
          <div class="col-8">
            <q-input filled v-model="ifNoWhy2" label="If No Why?" type="text" ></q-input>
          </div>
        </div>

        <div class="row">
          <div class="col-2">
            <p>Assets within 500mm Proved?</p>
          </div>
          <div class="col-2">
            <q-radio v-model="assetsWithin500mmProved" val="Yes" label="Yes"></q-radio>
            <q-radio v-model="assetsWithin500mmProved" val="No" label="No"></q-radio>
          </div>
          <div class="col-8">
            <p><b>(STOP THE JOB IF YOU CANNOT PROVE AN ASSET)</b></p>
          </div>
        </div>

        <!-- Section 6 -->

        <h2> Section 6 - Gas Detector and Readings</h2>
        <div class="form-section">
          <div class="row">
            <div class="col">
              <div class="subheading text-center"> Above the planned excavation area, <br/>before excavation commences</div>
            </div>
            <div class="col">
              <div class="subheading text-center"> Half way through the excavation (i.e at <br/>half the planned excavation depth)</div>
            </div>
            <div class="col">
              <div class="subheading text-center"> Once the main or service has been <br/>exposed</div>
            </div>
          </div>
          <div class="row">
            <div class="col">
              <q-input filled v-model.number="gasReading.beforeExcavation" label="Gas Reading %" type="number" suffix="%" step="0.1" min="0.0" max="100.0" :bg-color="getGasReadingColor(gasReading.beforeExcavation)"></q-input>
            </div>
            <div class="col">
              <q-input filled v-model.number="gasReading.middleExcavation" label="Gas Reading %" type="number" suffix="%" step="0.1" min="0.0" max="100.0" :bg-color="getGasReadingColor(gasReading.middleExcavation)"></q-input>
            </div>
            <div class="col">
              <q-input filled v-model.number="gasReading.exposedMain" label="Gas Reading %" type="number" suffix="%" step="0.1" min="0.0" max="100.0" :bg-color="getGasReadingColor(gasReading.exposedMain)"></q-input>
            </div>
          </div>

        </div>

        <!-- Section 7-->
        <h2> Section 7 - Pre-Start Meeting Attendees</h2>
        <div class="form-section">
          <cite> ! By signing this pre-start meeting record, you are confirming that you are fit for duty, not adversely affected by fatigue
            and meet Downer's drug and alcohol policy requirements.</cite>
          <div class="row">
            <div class="col">
              <div v-for="(attendee, index) in attendees" :key="attendee.id">
                <q-input filled v-model="attendees[index]" label="Insert Name"></q-input>

              </div>
              <q-btn @click="attendees.push('')">Add</q-btn>
              <q-btn @click="attendees.splice(index, 1)">Remove</q-btn>

            </div>
            <div class="col">
              <canvas id="signature"></canvas>
            </div>
          </div>
          <div class="row">
            <b>Responsible Crew Leader Declaration:</b>
            <cite>I confirm that the hazards, risks and controls associated with the activities scheduled
              for me today have been discussed with and are understood by the above attendees</cite>
          </div>
          <div class="row">
            <div class="col">
                <q-input filled v-model="crewLeader" label="Insert Name"></q-input>
            </div>

            <div class="col">
              <canvas id="signature"></canvas>
            </div>
          </div>

          <div class="row" id="noPrint">
            <q-btn @click="saveToLocalStorage">Save To LocalStorage</q-btn>
            <q-btn @click="loadFromLocalStorage">Load From LocalStorage</q-btn>
            <q-btn @click="loadTagDates">Load Tag Dates</q-btn>
          </div>

        </div>
      </q-form>

    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import { get, set } from 'idb-keyval'

export default defineComponent({
  name: 'IndexPage',

  data () {
    return {
      preStartMeetingConductedBy: '',
      jobNumber: '',
      trafficRiskAssessmentNumber: '',
      date: '',
      time: '',
      address: '',
      emergencyEvacuationPointNominated: false,

      // Section 2
      permitNumbers: {
        'Electrical Permit': '',
        'Asset Permit': '',
        'Deep Excavation': '',
        'Client Permit Number': '',
        'Hot Work': '',
        'Confined Space': '',
        'No Go Zome (less than 0.5m)': '',
        Authority: ''
      },

      tagDates: {
        'Electrical Lead': '',
        'Fire Extinguisher': '',
        RCD: '',
        'Fusion Iron': '',
        'Gas Detector': '',
        'Electrofusion Box': '',
        'Washington Tester': '',
        'First Aid': ''
      },

      // Section 4
      swmsUnderstoodByAllPersonnel: undefined,
      swms: {
        'Working on near pressurised gas distribution mains or piping': false,
        'Confined Space': false,
        'Working in the vicinity of moving mobile plant': false,
        'Working near traffic': false,
        'Working near to energised electrical assets': false,
        'Excavation and trenching greater than 1.5m': false,
        'People or objects falling greater than 2m from height': false,
        'Discovery, removal or disturbance of Asbestos': false,
        'Crane operation and lifting equipment': false
      },
      whyNot: '',
      personAssignedAsSpotter: '',

      // Section 5
      undergroundServices: {
        'Cables running down poles': '',
        'Traffic signal cables': '',
        'Substation cables HV and LV': '',
        'Drainage Pits': '',
        'Recycled water main': '',
        'Industrial piping': '',
        'Power to outdoor lighting': '',
        'Service pits': '',
        'NBN pits': '',
        'Sewer pits or pipes': '',
        'Potable water mains': '',
        'Recycled water service': '',
        'Power to spas, pools': '',
        'Power to electric gates': '',
        'Storm water pits or pipes': '',
        'Railway signal cables': '',
        'Fire hydrants': '',
        'Potable water services': '',
        'Underground storage tanks': '',
        'Power to units or bungalows': '',
        'Sprinkler systems': '',
        'Height of machine (m)': '',
        'Lowest cable (m)': ''

      },
      passiveSweepWithLocator: undefined,
      assetsWithin500mmLocated: undefined,
      assetsWithin500mmProved: undefined,

      ifNoWhy1: '',
      ifNoWhy2: '',

      // Section 6
      gasReading: {
        beforeExcavation: undefined,
        middleExacavation: undefined,
        exposedMain: undefined
      },

      // Section 7
      attendees: [''],
      crewLeader: ''
    }
  },

  // Anything within here will run when your page is first loaded.
  // Kind of like a setup function... do shit when page first loads.
  //
  mounted () {

    // Your other initialization code that's already here...

    // Create an interval timer that triggers the saveToLocalsStorage function every 10 seconds.
    // setInterval(this.saveToLocalStorage, 10000);

    // Get our HTML element that will hold the signature.
    // %%% const canvas = document.querySelector("#signature");

    // Setup our signature pad by passing into the Canvas.
    // TODO: Learn about Javascript Classes.
    // %%% const signaturePad = new SignaturePad(canvas);
  },

  created () {
    // Get a reference to the title element using a CSS selector.
    const titleElement = document.querySelector('title')

    // Get the current date as an ISO string.
    // TODO: You probably want to find a way to convert this to YYYY-MM-DD format.
    const currentDate = new Date().toISOString()

    // Set the text content of the title element.
    titleElement.innerText = `Job Sheet - ${currentDate}`
  },

  methods: {
    tagDateExpiry: function (tagDate) {
      // Wrap the tag date in Moment.JS Format.
      const tagDateInMomentFormat = moment(tagDate) // Some date from your form

      // Get today's date.
      const todaysDate = moment(Date.now())

      // Get today's date and subtract seven days from it.
      const oneWeekBeforeToday = moment(Date.now()).add(7, 'd')

      // If the tag date is more than today's date.
      if (tagDateInMomentFormat < todaysDate) {
        return 'negative'
      }

      // If the tag's date is more than one week before today's date...
      if (tagDateInMomentFormat < oneWeekBeforeToday) {
        // ... give the input a negative (red) color.
        // NOTE: For a list of colors, see: https://quasar.dev/style/color-palette
        return 'yellow-12'
      }

      // Otherwise, we just return the default color of the input (grey or whatever).
      return 'default'
    },

    getAssetColor: function (quantity) {
      if (quantity > 0) {
        return 'positive'
      }

      return 'default'
    },

    getGasReadingColor: function (reading) {
      if (typeof reading === 'undefined') {
        return
      }

      if (reading > 0) {
        return 'negative'
      }

      return 'positive'
    },

    saveToLocalStorage: async function () {
      // Choose a list of fields to save.
      const fieldsToSaveToPreStart = {
        preStartMeetingConductedBy: this.preStartMeetingConductedBy,
        jobNumber: this.jobNumber,
        trafficRiskAssessmentNumber: this.trafficRiskAssessmentNumber,
        address: this.address,
        permitNumbers: this.permitNumbers,
        swmsUnderstoodByAllPersonnel: this.swmsUnderstoodByAllPersonnel,
        swms: this.swms,
        personAssignedAsSpotter: this.personAssignedAsSpotter,
        undergroundServices: this.undergroundServices,
        gasReading: this.gasReading,
        attendees: this.attendees,
        crewLeader: this.crewLeader,
        passiveSweepWithLocator: this.passiveSweepWithLocator,
        assetsWithin500mmLocated: this.assetsWithin500mmLocated,
        assetsWithin500mmProved: this.assetsWithin500mmProved

        // etc...
      }

      const fieldsToSaveTagDates = {
        tagDates: this.tagDates
      }

      const fieldsToSaveJobDetails = {
        jobNumber: this.jobNumber,
        address: this.address
      }

      // We need to convert the data to a JSON 'string' in order to save it into localStorage.
      const fieldsToSaveToPreStartAsString = JSON.stringify(fieldsToSaveToPreStart)
      const fieldsToSaveTagDatesAsString = JSON.stringify(fieldsToSaveTagDates)
      const fieldsToSaveJobDetailsAsString = JSON.stringify(fieldsToSaveJobDetails)

      // Save it to local storage with key "savedForm".
      await set('savedForm-PreStart', fieldsToSaveToPreStartAsString)
      await set('savedForm-tagDates', fieldsToSaveTagDatesAsString)
      await set('savedForm-jobDetails', fieldsToSaveJobDetailsAsString)
    },

    loadFromLocalStorage: async function () {
      // Load the form from Local Storage (this will be a string at the moment).
      const savedPreStartFormAsString = await get('savedForm-PreStart')
      const savedTagDatesFormAsString = await get('savedForm-tagDates')
      const savedJobDetailsFormAsString = await get('savedForm-jobDetails')

      // Parse that string into a JSON obect.
      const savedPreStartFormAsObject = JSON.parse(savedPreStartFormAsString)
      const savedTagDatesFormAsObject = JSON.parse(savedTagDatesFormAsString)
      const savedJobDetailsFormAsObject = JSON.parse(savedJobDetailsFormAsString)
      // This is a bit of a shortcut because I'm lazy.
      // It will "merge" your items in the savedFormAsObject into your "data()" properties automatically.
      // But you could just set each field manually.
      // e.g.
      // this.permitNumbers = savedFormAsObject.permitNumbers;
      // etc
      Object.assign(this, savedPreStartFormAsObject)
      Object.assign(this, savedTagDatesFormAsObject)
      Object.assign(this, savedJobDetailsFormAsObject)
    },

    loadTagDates: async function () {
      const savedTagDatesFormAsString = await get('savedForm-tagDates')
      const savedTagDatesFormAsObject = JSON.parse(savedTagDatesFormAsString)
      Object.assign(this, savedTagDatesFormAsObject)
    }
  }
})
</script>

<style>
body {
  padding: 0px 10px 0px 10px;
}

#container {
  width: 1280px;
  max-width: 100%;
  margin: auto;
}

h1 {
  font-size: 3em;
  font-weight: bold;
}

h2 {
  font-size: 2em;
  font-weight: bold;
  text-transform: uppercase;
}

.subheading {
  font-size: 1em;
  font-weight: bold;
}

.form-section .row {
  margin-bottom: 0.25em;
}

.q-field {
  padding: 5px;
}



.q-input {
  font-family: arial black;
  font-size: 1.5em;
  text-transform: uppercase;
}

input[type="date"]::-webkit-input-placeholder { /* Chrome/Opera/Safari */

  color: white;

}

::-moz-placeholder { /* Firefox 19+ */

  color: white;

}

:-ms-input-placeholder { /* IE 10+ */

  color: white;

}

:-moz-placeholder { /* Firefox 18- */

  color: white;

}

* {
    -webkit-print-color-adjust: exact !important;   /* Chrome, Safari, Edge */
    color-adjust: exact !important;                 /*Firefox*/
}

@media print {
   #noPrint {
      visibility: hidden;
   }
}

</style>
