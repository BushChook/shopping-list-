<template>
  <q-page class="flex flex-center">
    <div id="container">
        <h1>TRAFFIC MANAGEMENT</h1>

        <q-form class="q-gutter-md">
          <div class="form-section">
            <div class="row">
              <div class="col-4">
                <q-input
                  filled
                  v-model="jobNumber"
                  label="Job Number"
                ></q-input>
              </div>
              <div class="col">
                <q-input filled v-model="address" label="Address"></q-input>
              </div>
            </div>

            <!--Part 1-->

            <div class="row">
              <h4>1. Third Party Traffic Management Assessment</h4>
              </div>
            </div>
            <div class="row">
              <div class="col">
                <div>
                  Traffic Management Contractor being utilised?
                </div>
                <q-btn-toggle v-model="trafficManagementContractorBeingUtilised" class="my-custom-toggle" no-caps unelevated toggle-color="primary"
                push glossy :options="[ {label: 'YES', value: 'one'}, {label: 'NO', value: 'two'}]"/>
              </div>
              <div class="col">
                <div>
                  Contractor Traffic Management JSA in use, sighted and signed?
                </div>
                <q-btn-toggle v-model="jsaInUse" class="my-custom-toggle" no-caps unelevated toggle-color="primary"
                push glossy :options="[ {label: 'YES', value: 'one'}, {label: 'NO', value: 'two'}]"/>
              </div>
            </div>

            <div class="row">
              <div class="col">
                <div>
                  Contractor site specific TMP in place?
                </div>
                <q-btn-toggle v-model="contractorSiteSpecificTmpInPlace" class="my-custom-toggle" no-caps unelevated toggle-color="primary"
                push glossy :options="[ {label: 'YES', value: 'one'}, {label: 'NO', value: 'two'}]"/>
              </div>
              <div class="col"/>
                <div>
                  Memorandum of Authorisation sighted?
                </div>
                <q-btn-toggle v-model="memorandumOfAuthorisationSighted" class="my-custom-toggle" no-caps unelevated toggle-color="primary"
                push glossy :options="[ {label: 'YES', value: 'one'}, {label: 'NO', value: 'two'}]"/>
            </div>

            <!--Part 2-->

            <h4>2. Traffic Management Assessment</h4>
            <div class="row">
              <div class="col-6">
                Road Type
                <q-btn-toggle
                v-model="roadType"
                color="brown"
                text-color="white"
                toggle-color="orange"
                toggle-text-color="black"
                rounded
                unelevated
                glossy
                :options="roadType1"
                @update:model-value="getDanger"
                />
              </div>




              <div class="col-6">
                Traffic Speed
                <q-btn-toggle
                v-model="trafficSpeed"
                color="brown"
                text-color="white"
                toggle-color="orange"
                toggle-text-color="black"
                rounded
                unelevated
                glossy
                :options="trafficSpeed1"
                @update:model-value="getDanger"
                />
              </div>
            </div>
            <div class="row">

              <div class="col">
                Clearence between workers and traffic
                <q-btn-toggle
                v-model="clearenceBetweenWorkers"
                color="brown"
                text-color="white"
                toggle-color="orange"
                toggle-text-color="black"
                rounded
                unelevated
                glossy
                :options="clearenceBetweenWorkers1"
                @update:model-value="getDanger"
                />
              </div>



              <div class="col">
                Task Duration
                <q-btn-toggle
                v-model="taskDuration"
                color="brown"
                text-color="white"
                toggle-color="orange"
                toggle-text-color="black"
                rounded
                unelevated
                glossy
                :options="taskDuration1"
                />
              </div>
            </div>
            <div class="row">
              <div class="col">
                Site Risk Rating
                <q-slider
                class="q-mt-xl"
                v-model="siteRiskRating"
                :color="getColorForSlider()"
                label-hidden
                markers
                :marker-labels="trafficSliderSafetyLabels"
                :min="1"
                :max="14"
                @update:model-value="getDanger"
                />
              </div>
            </div>

            <!--Part 3-->

            <h4>3. Additional Risks / Hazards</h4>
            <div class="row">
              <div class="col">
                <div>
                  Traffic Volume At The Worksite
                </div>
                <q-btn-toggle
                v-model="trafficVolume"
                color="brown"
                text-color="white"
                toggle-color="orange"
                toggle-text-color="black"
                rounded
                unelevated
                glossy
                :options="trafficVolume1"/>
              </div>
              <div class="col">
                <div>
                  Is there rough or unsealed surfaces?
                </div>
                <q-btn-toggle v-model="roughOrUnsealedSurfaces" class="my-custom-toggle" no-caps unelevated toggle-color="primary"
                push glossy :options="[ {label: 'YES', value: 'one'}, {label: 'NO', value: 'two'}]"/>
              </div>
            </div>
            <div class="row">
              <div class="col">
                <div>
                  Are there pedestrians through the work site?
                </div>
                <q-btn-toggle v-model="pedestriansThroughTheWorkSite" class="my-custom-toggle" no-caps unelevated toggle-color="primary"
                push glossy :options="[ {label: 'YES', value: 'one'}, {label: 'NO', value: 'two'}]"/>
              </div>
              <div class="col">
                <div>
                  Is there poor advance sight distance to the work site (e.g. bends, crest, fog, etc)?
                </div>
                <q-btn-toggle v-model="siteDistance" class="my-custom-toggle" no-caps unelevated toggle-color="primary"
                push glossy :options="[ {label: 'YES', value: 'one'}, {label: 'NO', value: 'two'}]"/>
              </div>
            </div>
            <div id="hazards">
             <q-input v-model="additionalHazards" filled type="textarea" input-style="min-height:10em;" label="Additional Hazards"></q-input>
            </div>

            <!--Part 4-->

            <h4>4. Controls</h4>
            <div class="row">
              <div class="col">
                <div>
                  Reduction of speed at the work site?
                </div>
                <q-btn-toggle
                v-model="reductionOfSpeed"
                push
                glossy
                toggle-color="primary"
                :options="[
                  {label: 'YES', value: 'one'},
                  {label: 'NO', value: 'two'},
                ]"
              />
              </div>
              <div class="col">
                <div>
                  Traffic controllers required?
                </div>
                <q-btn-toggle
                v-model="trafficControllersRequired"
                push
                glossy
                toggle-color="primary"
                :options="[
                  {label: 'YES', value: 'one'},
                  {label: 'NO', value: 'two'},
                ]"
              />
              </div>
            </div>

            <div class="row">
              <div class="col">
                <div>
                  Road Closure?
                </div>
                <q-btn-toggle
                v-model="roadClosure"
                push
                glossy
                toggle-color="primary"
                :options="[
                  {label: 'YES', value: 'one'},
                  {label: 'NO', value: 'two'},
                ]"
              />
              </div>
              <div class="col">
                <div>
                  Traffic Management Plan required?
                </div>
                <q-btn-toggle
                v-model="tmpPlanRequired"
                push
                glossy
                toggle-color="primary"
                :options="[
                  {label: 'YES', value: 'one'},
                  {label: 'NO', value: 'two'},
                ]"
              />
              </div>
            </div>

            <div class="row">
              <div class="col-6">
                <div>
                  Memorandum of Consent (MOA) required?
                </div>
                <q-btn-toggle
                v-model="moaRequired"
                push
                glossy
                toggle-color="primary"
                :options="[
                  {label: 'YES', value: 'one'},
                  {label: 'NO', value: 'two'},
                ]"
              />
              </div>
              <div class="col-2">
                Generic TMP no:
                <q-select standout="bg-teal text-white" v-model="trafficManagementPlan" :options="tmpOptions" label="Custom standout" />
              </div>
              <div class="col-2">
                Site Specific:
                <q-select standout="bg-teal text-white" v-model="model" :options="options" label="Custom standout" />
              </div>
            </div>

            <div class="row">
              <div class="col">
                <div>
                  Pedestrian Traffic Management Required?
                </div>
                <q-btn-toggle
                v-model="pedestrianTmpRequired"
                push
                glossy
                toggle-color="primary"
                :options="[
                  {label: 'YES', value: 'one'},
                  {label: 'NO', value: 'two'},
                ]"
              />
              </div>
              <div class="col">
                <div>
                  Does Generic TMP require modification?
                </div>
                <q-btn-toggle
                v-model="tmpRequireModification"
                push
                glossy
                toggle-color="primary"
                :options="[
                  {label: 'YES', value: 'one'},
                  {label: 'NO', value: 'two'},
                ]"
              />
              </div>
            </div>

            <!--Part 5-->
            <h4>5. Declaration</h4>
            <div class="row">
              <b>Responsible Crew Leader Declaration:</b>
              <cite>I confirm that the hazards, risks and controls associated with the activities scheduled
                for me today have been discussed with and are understood by the above attendees</cite>
            </div>

            <div class="row">
              <div class="col">
                <q-input filled v-model="crewLeader" label="Insert Name"></q-input>
              </div>
            </div>

            <div class="row" id="noPrint">
              <q-btn @click="saveToLocalStorage">Save To LocalStorage</q-btn>
              <q-btn @click="loadFromLocalStorage">Load From LocalStorage</q-btn>
            </div>
        </q-form>
      </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'TrafficForm',

  data() {
    return {
      jobNumber: "",
      address: "",

      //Part 1

      tmpOptions: [],
      trafficManagementContractorBeingUtilised: "",
      jsaInUse: "",
      contractorSiteSpecificTmpInPlace: "",
      memorandumOfAuthorisationSighted:"",

      //Part 2
      roadType:"",
      roadType1:[
        {value: 'Local', label: 'Local'},
        {value: 'Collector', label: 'Collector'},
        {value: 'Secondary', label: 'Secondary'},
        {value: 'Arterial', label: 'Arterial'},
        {value: 'Freeway', label: 'Freeway'}
      ],

      trafficSpeed:"",
      trafficSpeed1:[
        {label: '40', value: '40'},
        {label: '50', value: '50'},
        {label: '60', value: '60'},
        {label: '70', value: '70'},
        {label: '80', value: '80'},
        {label: '90', value: '90'},
        {label: '100', value: '100'},
        {label: '110', value: '110'}
      ],

      clearenceBetweenWorkers:"",
      clearenceBetweenWorkers1:  [
        {label: '<1.2m', value: '<1.2m'},
        {label: '1.2 - 3m', value: '1.2 - 3m'},
        {label: '3 - 9m', value: '3 - 9m'},
        {label: '>9m', value: '>9m'}
      ],

      taskDuration:"",
      taskDuration1:  [
      {value: '<5 mins', label: '<5 mins'},
      {value: '<20 mins', label: '<20 mins'},
      {value: 'Short Term Work', label: 'Short Term Work'},
      {value: 'Long Term Work', label: 'Long Term Work'}
      ],

      siteRiskRating: 0,
      trafficSliderSafetyLabels: [
      { value: 3, label: 'Low' },
      { value: 6, label: 'Medium' },
      { value: 9, label: 'High' },
      { value: 12, label: 'Very High' }
      ],

      // Part 3
      trafficVolume:"",
      trafficVolume1:[
      {label: 'Low', value: 'Low'},
      {label: 'Medium', value: 'Medium'},
      {label: 'High', value: 'High'},
      {label: 'Very High', value: 'Very High'}
      ],

      roughOrUnsealedSurfaces: "",
      pedestriansThroughTheWorkSite:"",
      siteDistance:"",

      //Part 4
      reductionOfSpeed:"",
      trafficControllersRequired: "",
      roadClosure:"",
      tmpPlanRequired:"",
      moaRequired:"",
      pedestrianTmpRequired:"",
      tmpRequireModification:"",
      trafficManagementPlan: "001",

      //Part 5
      crewLeader:'',
    };
  },

  methods:{
    getColorForSlider: function () {
      if(this.siteRiskRating <=5) {
        return 'green';
      }
      else if (this.siteRiskRating <=8){
      return 'yellow';
      }
      else if(this.siteRiskRating <=11){
      return 'orange';
      }
      else if(this.siteRiskRating >=12){
      return 'red';
      }
    },

    getDanger: function(){

      if(!this.trafficSpeed || !this.roadType || !this.clearenceBetweenWorkers)
      {return;}

      const lookupTable = {
        40: {
          "Local": {
            '<1.2m': 4,
            '1.2 - 3m': 3,
            '3 - 9m': 2,
            '>9m': 2,
          },
          "Collector": {
            '<1.2m': 7,
            '1.2 - 3m': 5,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Secondary":{
            '<1.2m': 7,
            '1.2 - 3m': 5,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Arterial":{
            '<1.2m': 7,
            '1.2 - 3m': 6,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Freeway": {
            '<1.2m': 9,
            '1.2 - 3m': 6,
            '3 - 9m': 3,
            '>9m': 2,
          }
        },
        50: {
          "Local": {
            '<1.2m': 5,
            '1.2 - 3m': 4,
            '3 - 9m': 2,
            '>9m': 1,
          },
          "Collector": {
            '<1.2m': 8,
            '1.2 - 3m': 4,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Secondary":{
            '<1.2m': 8,
            '1.2 - 3m': 5,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Arterial":{
            '<1.2m': 9,
            '1.2 - 3m': 7,
            '3 - 9m': 6,
            '>9m': 2,
          },
          "Freeway": {
            '<1.2m': 10,
            '1.2 - 3m': 8,
            '3 - 9m': 6,
            '>9m': 2,
          }
        },
        60: {
          "Local": {
            '<1.2m': 6,
            '1.2 - 3m': 4,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Collector": {
            '<1.2m': 8,
            '1.2 - 3m': 5,
            '3 - 9m': 4,
            '>9m': 2,
          },
          "Secondary":{
            '<1.2m': 11,
            '1.2 - 3m': 7,
            '3 - 9m': 4,
            '>9m': 3,
          },
          "Arterial":{
            '<1.2m': 11,
            '1.2 - 3m': 7,
            '3 - 9m': 4,
            '>9m': 3,
          },
          "Freeway": {
            '<1.2m': 12,
            '1.2 - 3m': 10,
            '3 - 9m': 6,
            '>9m': 3,
          }
        },
        70: {
          "Local": {
            '<1.2m': 6,
            '1.2 - 3m': 4,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Collector": {
            '<1.2m': 8,
            '1.2 - 3m': 5,
            '3 - 9m': 4,
            '>9m': 2,
          },
          "Secondary":{
            '<1.2m': 11,
            '1.2 - 3m': 7,
            '3 - 9m': 4,
            '>9m': 3,
          },
          "Arterial":{
            '<1.2m': 11,
            '1.2 - 3m': 7,
            '3 - 9m': 4,
            '>9m': 3,
          },
          "Freeway": {
            '<1.2m': 12,
            '1.2 - 3m': 10,
            '3 - 9m': 6,
            '>9m': 3,
          }
        },
        80: {
          "Local": {
            '<1.2m': 8,
            '1.2 - 3m': 5,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Collector": {
            '<1.2m': 11,
            '1.2 - 3m': 7,
            '3 - 9m': 4,
            '>9m': 2,
          },
          "Secondary":{
            '<1.2m': 12,
            '1.2 - 3m': 10,
            '3 - 9m': 6,
            '>9m': 2,
          },
          "Arterial":{
            '<1.2m': 13,
            '1.2 - 3m': 10,
            '3 - 9m': 8,
            '>9m': 6,
          },
          "Freeway": {
            '<1.2m': 13,
            '1.2 - 3m': 11,
            '3 - 9m': 9,
            '>9m': 6,
          }
        },
        90: {
          "Local": {
            '<1.2m': 8,
            '1.2 - 3m': 5,
            '3 - 9m': 3,
            '>9m': 2,
          },
          "Collector": {
            '<1.2m': 11,
            '1.2 - 3m': 7,
            '3 - 9m': 4,
            '>9m': 2,
          },
          "Secondary":{
            '<1.2m': 12,
            '1.2 - 3m': 10,
            '3 - 9m': 6,
            '>9m': 2,
          },
          "Arterial":{
            '<1.2m': 13,
            '1.2 - 3m': 10,
            '3 - 9m': 8,
            '>9m': 6,
          },
          "Freeway": {
            '<1.2m': 13,
            '1.2 - 3m': 11,
            '3 - 9m': 9,
            '>9m': 6,
          }
        },
        100: {
          "Local": {
            '<1.2m': 12,
            '1.2 - 3m':9,
            '3 - 9m': 7,
            '>9m': 5,
          },
          "Collector": {
            '<1.2m': 13,
            '1.2 - 3m': 11,
            '3 - 9m': 9,
            '>9m': 6,
          },
          "Secondary":{
            '<1.2m': 13,
            '1.2 - 3m':11,
            '3 - 9m': 9,
            '>9m': 7,
          },
          "Arterial":{
            '<1.2m': 14,
            '1.2 - 3m': 12,
            '3 - 9m': 10,
            '>9m': 7,
          },
          "Freeway": {
            '<1.2m': 14,
            '1.2 - 3m': 13,
            '3 - 9m': 12,
            '>9m': 8,
          }
        },
        110: {
          "Local": {
            '<1.2m': 12,
            '1.2 - 3m':9,
            '3 - 9m': 7,
            '>9m': 5,
          },
          "Collector": {
            '<1.2m': 13,
            '1.2 - 3m': 11,
            '3 - 9m': 9,
            '>9m': 6,
          },
          "Secondary":{
            '<1.2m': 13,
            '1.2 - 3m':11,
            '3 - 9m': 9,
            '>9m': 7,
          },
          "Arterial":{
            '<1.2m': 14,
            '1.2 - 3m': 12,
            '3 - 9m': 10,
            '>9m': 7,
          },
          "Freeway": {
            '<1.2m': 14,
            '1.2 - 3m': 13,
            '3 - 9m': 12,
            '>9m': 8,
          }
        },
      }

      this.siteRiskRating = lookupTable[this.trafficSpeed][this.roadType][this.clearenceBetweenWorkers];
    },

    saveToLocalStorage: function()
    {
      // Choose a list of fields to save.
      const fieldsToSave = {

        //part 1
        jobNumber: this.jobNumber,
        address: this.address,
        trafficManagementPlan: this.trafficManagementPlan,
        tmpOptions: this.tmpOptions,
        trafficManagementContractorBeingUtilised: this.trafficManagementContractorBeingUtilised,
        jsaInUse: this.jsaInUse,
        contractorSiteSpecificTmpInPlace: this.contractorSiteSpecificTmpInPlace,
        memorandumOfAuthorisationSighted: this.memorandumOfAuthorisationSighted,

        //part 3
        trafficVolume: this.trafficVolume,
        trafficVolume1: this.trafficVolume1,
        roughOrUnsealedSurfaces: this.roughOrUnsealedSurfaces,
        pedestriansThroughTheWorkSite: this.pedestriansThroughTheWorkSite,
        siteDistance: this.siteDistance,

        //part 4
        reductionOfSpeed:this.reductionOfSpeed,
        trafficControllersRequired: this.trafficControllersRequired,
        roadClosure: this.roadClosure,
        tmpPlanRequired: this.tmpPlanRequired,
        moaRequired: this.moaRequired,
        pedestrianTmpRequired: this.pedestrianTmpRequired,
        tmpRequireModification: this.tmpRequireModification,

        //part 5
        crewLeader: this.crewLeader,
        // etc...
      };

      // We need to convert the data to a JSON 'string' in order to save it into localStorage.
      const fieldsToSaveAsTrafficString = JSON.stringify(fieldsToSave);

      // Save it to local storage with key "savedForm".
      window.localStorage.setItem('savedForm', fieldsToSaveAsTrafficString);
    },

    loadFromLocalStorage: function()
    {
      // Load the form from Local Storage (this will be a string at the moment).
      const savedFormAsString = window.localStorage.getItem('savedForm');
      const savedJobDetailsFormAsString = window.localStorage.getItem('savedForm-jobDetails');

      // Parse that string into a JSON obect.
      const savedFormAsObject = JSON.parse(savedFormAsString);
      const savedJobDetailsFormAsObject = JSON.parse(savedJobDetailsFormAsString);
      // This is a bit of a shortcut because I'm lazy.
      // It will "merge" your items in the savedFormAsObject into your "data()" properties automatically.
      // But you could just set each field manually.
      // e.g.
      // this.oermitNumbers = savedFormAsObject.permitNumbers;
      // etc
      Object.assign(this, savedFormAsObject);
      Object.assign(this, savedJobDetailsFormAsObject);
    },
  },

  // This function is run before the HTML has been rendered.
  created() {
    // Setup a function to "pad" the numbers.
    const pad = function(num, size) {
      num = num.toString();
      while (num.length < size) num = "0" + num;
      return num;
    }

    // Loop through numbers 0 to 30.
    for(let i = 1; i < 30; i++) {
      // Pad the number of 'i'.
      const paddedNumber = pad(i, 3);

      // Add this padded number to our list of TMP options.
      this.tmpOptions.push(paddedNumber)
    }
    // Get a reference to the title element using a CSS selector.
    const titleElement = document.querySelector('title');

    // Get the current date as an ISO string.
    // TODO: You probably want to find a way to convert this to YYYY-MM-DD format.
    const currentDate = new Date().toISOString();

    // Set the text content of the title element.
    titleElement.innerText = `Traffic Management - ${currentDate}`;
  }
});
</script>

<style>
    body {
      padding: 0px 10px 0px 10px;
    }
    .q-field {
      padding: 5px;
    }

    #container {
      width: 1280px;
      max-width: 100%;
      margin: auto;

    }

    .q-input {
      font-family: arial black;
      font-size: 1.5em;
      text-transform: uppercase;
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
