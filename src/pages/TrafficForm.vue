<template>
  <q-page class="flex flex-center">
    <div id="container">
        <h1>TRAFFIC MANAGEMENT</h1>

        <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
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
             <q-input v-model="additionalHazards" filled type="textarea" input-style="min-height:10em;" label="Addional Hazards"></q-input>
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
  name: 'TrafficForm'
})
</script>
