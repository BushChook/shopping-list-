<template>
  <q-page class="flex flex-center">
    <div id="container">
        <h1>Daily Plant Inspection Form</h1>
        <q-form class="q-gutter-md">
          <!--Part 1-->
          <h3>1. Plant Type:</h3>
          <div class="row">
            <div v-for="(ignore,type) in plantType" class="col-3">
              <q-checkbox v-model="plantType[type]" :label="type"></q-checkbox>
            </div>
          </div>
          <div class="row">
            <div class="col-3">
              <q-input filled v-model="Other" label="Other"></q-input>
            </div>
          </div>

          <!--Part 2-->
          <h3>2. Plant Details</h3>
          <div class="row">
            <div class="col">
              <q-input
                filled
                v-model="startDate"
                label="Start Date"
                type="date"
                stack-label
              ></q-input>
              <q-input filled v-model="make" label="Make"></q-input>
              <q-input filled v-model="model" label="Model"></q-input>
            </div>

            <div class="col">
              <q-input
                filled
                v-model="siteLocation"
                label="Site/Location"
              ></q-input>
              <q-input
                filled
                v-model="registration"
                label="Registration"
              ></q-input>
            </div>
          </div>

          <!-- Part 3-->
          <h3>3. Daily Pre Start Checks</h3>
          <div class="form-section">
            <div
              class="q-markup-table q-table__container q-table__card q-table--cell-separator q-table--flat q-table--bordered"
            >
              <table class="q-table">
                <thead>
                  <tr>
                    <th style="width: 50%"></th>
                    <th>MONDAY</th>
                    <th>TUESDAY</th>
                    <th>WEDNESDAY</th>
                    <th>THURSDAY</th>
                    <th>FRIDAY</th>
                    <th>SATURDAY</th>
                    <th>SUNDAY</th>
                  </tr>
                  <tr>
                    <th>PLANT HOURS / KILOMETRES</th>
                    <th></th>
                    <th></th>
                    <th></th>
                    <th></th>
                    <th></th>
                    <th></th>
                    <th></th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <th id="tableHeaders">General Checks</th>
                  </tr>

                  <tr>
                    <th>(Fluids) Fuel, oil, battery, hydraulics, coolant</th>
                    <th v-for="(value, dayOfTheWeek) in fluids" :class="getChecklistBackgroundColor(fluids[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="fluids[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(fluids[dayOfTheWeek])"
                        :keep-color="true"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>(Visibility) Windscreen, wipers, washer, mirrors</th>
                    <th v-for="(value, dayOfTheWeek) in visibility" :class="getChecklistBackgroundColor(visibility[dayOfTheWeek])">
                      <q-toggle
                        toggle-indeterminate
                        v-model="visibility[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(visibility[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Cabin) Access/egress, seating, seatbelts, loose objects
                    </th>
                    <th v-for="(value, dayOfTheWeek) in cabin" :class="getChecklistBackgroundColor(cabin[dayOfTheWeek])">
                      <q-toggle
                        toggle-indeterminate
                        v-model="cabin[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(cabin[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>(Wheels) Tyres, nuts, damage, pressure</th>
                    <th v-for="(value, dayOfTheWeek) in wheels" :class="getChecklistBackgroundColor(wheels[dayOfTheWeek])">
                      <q-toggle
                        toggle-indeterminate
                        v-model="wheels[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(wheels[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>(Guards) In place, secure, warning signs</th>
                    <th v-for="(value, dayOfTheWeek) in guards" :class="getChecklistBackgroundColor(guards[dayOfTheWeek])">
                      <q-toggle
                        toggle-indeterminate
                        v-model="guards[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(guards[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Warning Devices) Check lights, horn & motion beepers are
                      working
                    </th>
                    <th v-for="(value, dayOfTheWeek) in warningDevices" :class="getChecklistBackgroundColor(warningDevices[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="warningDevices[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(warningDevices[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Load Cart) Check load capacity plate is fitted, legible &
                      correct
                    </th>
                    <th v-for="(value, dayOfTheWeek) in loadCart" :class="getChecklistBackgroundColor(loadCart[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="loadCart[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(loadCart[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Brakes) Check brakes & park brake for proper operation
                    </th>
                    <th v-for="(value, dayOfTheWeek) in brakes" :class="getChecklistBackgroundColor(brakes[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="brakes[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(brakes[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>(Body) Check body of plant for any damage</th>
                    <th v-for="(value, dayOfTheWeek) in body" :class="getChecklistBackgroundColor(body[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="body[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(body[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Controls) After start up check steering, pedals &
                      controls are in good order
                    </th>
                    <th v-for="(value, dayOfTheWeek) in controls" :class="getChecklistBackgroundColor(controls[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="controls[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(controls[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Hydraulics) Check hydraulic cylinders, hoses for leaks
                    </th>
                    <th v-for="(value, dayOfTheWeek) in hydraulics" :class="getChecklistBackgroundColor(hydraulics[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="hydraulics[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(hydraulics[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Engine/Exhaust) Check guarded adequately to protect from
                      burns
                    </th>
                    <th v-for="(value, dayOfTheWeek) in engineExhaust" :class="getChecklistBackgroundColor(engineExhaust[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="engineExhaust[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(engineExhaust[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Fire Extinguisher) Check vehicle is fitted with a fire
                      extinguisher
                    </th>
                    <th v-for="(value, dayOfTheWeek) in fireExtinguisher" :class="getChecklistBackgroundColor(fireExtinguisher[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="fireExtinguisher[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(fireExtinguisher[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr>
                    <th>
                      (Other) Other manufacturers requirement. Detail in
                      "Section 4"
                    </th>
                    <th v-for="(value, dayOfTheWeek) in otherRequirement" :class="getChecklistBackgroundColor(otherRequirement[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="otherRequirement[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(otherRequirement[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Fork lift'] === true">
                    <th id="tableHeaders">Forklift Specific</th>
                  </tr>

                  <tr v-if="plantType['Fork lift'] === true">
                    <th>(Tyres) Check forks for signs of damage</th>
                    <th v-for="(value, dayOfTheWeek) in tyres" :class="getChecklistBackgroundColor(tyres[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="tyres[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(tyres[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Fork lift'] === true">
                    <th>
                      (Operation) Check pedals & controls for smooth operation
                    </th>
                    <th v-for="(value, dayOfTheWeek) in operation" :class="getChecklistBackgroundColor(operation[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="operation[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(operation[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Fork lift'] === true">
                    <th>
                      (Jib) Check locating pins in correct position, safe and
                      fitted correctly
                    </th>
                    <th v-for="(value, dayOfTheWeek) in jib" :class="getChecklistBackgroundColor(jib[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="jib[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(jib[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Fork lift'] === true">
                    <th>(Safety Chains) Check for good condition</th>
                    <th v-for="(value, dayOfTheWeek) in safetyChains" :class="getChecklistBackgroundColor(safetyChains[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="safetyChains[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(safetyChains[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Fork lift'] === true">
                    <th>
                      (Shackle & Swivel) Check shackle securing swivel hook
                      correctly instally & tightened
                    </th>
                    <th v-for="(value, dayOfTheWeek) in shackleAndSwivel" :class="getChecklistBackgroundColor(shackleAndSwivel[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="shackleAndSwivel[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(shackleAndSwivel[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Skid Steer Loader'] === true || plantType['Golf Buggy'] === true || plantType['ATV']=== true">
                    <th id="tableHeaders">
                      Skid Steer Loader / Golf Buggy / ATV
                    </th>
                  </tr>

                  <tr v-if="plantType['Skid Steer Loader'] === true || plantType['Golf Buggy'] === true || plantType['ATV']=== true">
                    <th>(Decals) Check decals fitted</th>
                    <th v-for="(value, dayOfTheWeek) in decals" :class="getChecklistBackgroundColor(decals[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="decals[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(decals[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Skid Steer Loader'] === true || plantType['Golf Buggy'] === true || plantType['ATV']=== true">
                    <th>
                      (ROPS) Roller over protection system / protective
                      structure fitted "AS2294"
                    </th>
                    <th v-for="(value, dayOfTheWeek) in rops" :class="getChecklistBackgroundColor(rops[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="rops[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(rops[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Skid Steer Loader'] === true || plantType['Golf Buggy'] === true || plantType['ATV']=== true">
                    <th>
                      (Attach Points) Inspect attach points, connecting rods,
                      safety pins in good condition {{ value }}
                    </th>
                    <th v-for="(value, dayOfTheWeek) in attachPoints1" :class="getChecklistBackgroundColor(attachPoints1[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="attachPoints1[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(attachPoints1[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Excavator']=== true || plantType['Backhoe']=== true">
                    <th id="tableHeaders">Earthmoving Exacator / Backhoe</th>
                  </tr>

                  <tr v-if="plantType['Excavator']=== true || plantType['Backhoe']=== true">
                    <th>
                      (Tracks) Check condition, no obvious signs of damage to
                      treads/sprockets
                    </th>
                    <th v-for="(value, dayOfTheWeek) in tracks" :class="getChecklistBackgroundColor(tracks[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="tracks[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(tracks[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Excavator']=== true || plantType['Backhoe']=== true">
                    <th>
                      (Working Loads) Check safe working loads clearly marked
                    </th>
                    <th v-for="(value, dayOfTheWeek) in workingLoads" :class="getChecklistBackgroundColor(workingLoads[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="workingLoads[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(workingLoads[dayOfTheWeek])"
                      />
                    </th>
                  </tr>

                  <tr v-if="plantType['Excavator']=== true || plantType['Backhoe']=== true">
                    <th>
                      (Attach Points) Check condition attach points, quick
                      hitch, connecting rods, safety pins
                    </th>
                    <th v-for="(value, dayOfTheWeek) in attachPoints2" :class="getChecklistBackgroundColor(attachPoints2[dayOfTheWeek])">
                        <q-toggle
                        toggle-indeterminate
                        v-model="attachPoints2[dayOfTheWeek]"
                        label=""
                        :color="getChecklistColor(attachPoints2[dayOfTheWeek])"
                      />
                    </th>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>

          <!-- Part 4-->
          <h3> 4. Fault / Defect Report / manufacturers requirements</h3>
          <div class="form-section">
            <div class="row">
              <div class="col">
                <q-checkbox v-model="faultRectified" label="Fault rectified and safe to use"></q-checkbox>
              </div>
              <div class="col">
                <q-checkbox v-model="plantUnsafeToUse" label="Plant unsafe to use"></q-checkbox>
              </div>
            </div>
            <q-input v-model="faults" v-if="faultRectified || plantUnsafeToUse === true" filled type="textarea" input-style="min-height:10em;" label="Explain Why"></q-input>
          </div>

          <!-- Part 5-->
          <h3> 5. Declaration</h3>
          <cite> I, the operator, have completed the full check list herein and I have forwarded a copy of this report to the responsible person for fault rectification (if any).</cite>
          <div class="row">
            <div class="col">
              <q-input filled v-model="crewLeader1" label="Insert Name"></q-input>
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
import { defineComponent } from 'vue';
import { get, set } from 'idb-keyval';


export default defineComponent({
  name: 'PlantChecklist',
    data() {
          return {
            // Part 1
            plantType: {
              "Fork lift": false,
              "Hi AB Crane": false,
              Backhoe: false,
              Excavator: false,
              "Vibrating Plate/Wacker": false,
              "Skid Steer Loader": false,
              Compressor: false,
              "Truck / Trailer": false,
              Generator: false,
              "Golf Buggy": false,
              ATV: false,
            },
            Other: "",

            // Part 2
            startDate: "",
            make: "",
            model: "",
            siteLocation: "",
            registration: "",

            //Part 3
            fluids: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            visibility: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            cabin: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            wheels: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            guards: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            warningDevices: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            loadCart: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            brakes: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            body: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            controls: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            hydraulics: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            engineExhaust: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            fireExtinguisher: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            otherRequirement: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            tyres: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            operation: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            jib: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            safetyChains: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            shackleAndSwivel: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            decals: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            rops: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            attachPoints1: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            tracks: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            workingLoads: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            attachPoints2: {
              monday: "",
              tuesday: "",
              wednesday: "",
              thursday: "",
              friday: "",
              saturday: "",
              sunday: "",
            },

            // Part 4

            faultRectified: false,
            plantUnsafeToUse: false,

            //Part 5
            crewLeader1:'',


          };


        },

        methods: {

          getChecklistColor: function(value)
          {
            if(value === true) {
              return 'positive';
            }

            if(value === false) {
              return 'negative'
            }

            return 'default'
          },

          getChecklistBackgroundColor: function(value)
          {
            if(value === true) {
              return 'bg-green-1'
            }

            if(value === false) {
              return 'bg-red-2'
            }

            return 'bg-default'
          },




          saveToLocalStorage: async function()
          {
            // Choose a list of fields to save.
            const fieldsToSave = {
              startDate: this.startDate,
              plantType: this.plantType,
              make: this.make,
              model: this.model,
              siteLocation: this.siteLocation,
              registration: this.registration,

              fluids: this.fluids,
              visibility: this.visibility,
              cabin: this.cabin,
              wheels: this.wheels,
              guards: this.guards,
              warningDevices: this.warningDevices,
              loadCart: this.loadCart,
              brakes: this.brakes,
              body: this.body,
              controls: this.controls,
              hydraulics: this.hydraulics,
              engineExhaust: this.engineExhaust,
              fireExtinguisher: this.fireExtinguisher,
              other: this.other,

              tyres: this.tyres,
              operation: this.operation,
              jib: this.jib,
              safetyChains: this.safetyChains,
              shackleAndSwivel: this.shackleAndSwivel,

              decals: this.decals,
              rops: this.rops,
              attachPoints1: this.attachPoints1,

              tracks: this.tracks,
              workingLoads: this.workingLoads,
              attachPoints2: this.attachPoints2,

              crewLeader1: this.crewLeader1,
              // etc...
            };

            // We need to convert the data to a JSON 'string' in order to save it into localStorage.
            const fieldsToSaveAsString = JSON.stringify(fieldsToSave);

            // Save it to local storage with key "savedForm".
            await set('savedForm-PlantChecklist', fieldsToSaveAsString);
          },

          loadFromLocalStorage: async function()
          {
            // Load the form from Local Storage (this will be a string at the moment).
            const savedFormAsString = await get('savedForm-PlantChecklist');

            // Parse that string into a JSON obect.
            const savedFormAsObject = JSON.parse(savedFormAsString);

            // This is a bit of a shortcut because I'm lazy.
            // It will "merge" your items in the savedFormAsObject into your "data()" properties automatically.
            // But you could just set each field manually.
            // e.g.
            // this.permitNumbers = savedFormAsObject.permitNumbers;
            // etc
            Object.assign(this, savedFormAsObject);
          }
        },

        created() {
          // Get a reference to the title element using a CSS selector.
          const titleElement = document.querySelector('title');

          // Get the current date as an ISO string.
          // TODO: You probably want to find a way to convert this to YYYY-MM-DD format.
          const currentDate = new Date().toISOString();

          // Set the text content of the title element.
          titleElement.innerText = `Plant Checklist - ${currentDate}`;
        },
  })
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

    #tableHeaders {
      background-color: bisque;
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

    @media screen and (max-width: 1000px){
      body{
        font-size: .5em;
      }


      #container {
        width:900px;
        max-width: 100%;
        margin: auto;
      }

      .form-section {max-width: 100%; width: 900px;}

      h3{ font-size: 3em}
      .q-field {
        padding: 1px;
      }
    }
</style>
