<script setup>
import { reactive, ref } from 'vue'
const emit = defineEmits(['recording'])
 // const combined = 25
 defineProps({
   combined: Number
 });
 let data = reactive({
      projects: [
           {name: 'First one', id: 1},
           {name: 'Second one', id: 2},
           {name: 'Third one', id: 3},
           {name: 'Last one', id: 4}
      ],
      recordingOptions: {screen: true, video: { facingMode: "user", width: { min: 1280 },
    height: { min: 720 } }, audio: false},
      showModal: false,
      chosenProject: ''
})
 function showRecordingOptions()
 {
     data.showModal = true
 }
 function startRecording()
 {
      if(data.chosenProject == '' || data.chosenProject == undefined || data.chosenProject == null)
      {
           alert("Choose a project")
      }else{
           if (navigator.getUserMedia)
           {
                let stream = window.navigator.mediaDevices.getUserMedia(data.recordingOptions)
                .then( request => {
                    // console.log("streaming available")
                    emit('recording', request)
                })
                .catch( (err) => {
                     alert(err)
                     console.log(err)
                })
           }else{
                alert("Not available")
           }
      }
      
 }
 function closeModal()
 {
      data.showModal = false
 }
</script>
<template>
       <section class="bg-white py-4 my-2">
            <div class="flex justify-start items-center gap-52 mx-7">
                 <div>
                      <p class="text-sm text-gray-500 my-2 ">Snapbyte <span class="text-lg">&#8250;</span> My Recordings</p>
                      <h1 class="text-2xl">My Recordings <span class="text-gray-500 font-bold">{{combined}} </span></h1>
                 </div>
                 <ul class="flex jusify-center items-center gap-6">
                      <li class="flex justify-start items-center gap-2 border border-gray-200 rounded-full py-2 px-4 cursor-pointer">
                           <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4" />
                           </svg>
                           <span>By Date</span>
                      </li>
                      <li class="flex justify-start items-center gap-2 border border-gray-200 rounded-full py-2 px-4 cursor-pointer">
                           <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z" />
                           </svg>
                           <span>Add Filter</span>
                      </li>
                      <li class="flex justify-start items-center gap-2 rounded-full py-3 px-6 bg-teal-500 text-white cursor-pointer">
                           <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
                          </svg>
                           <span>New Request</span>
                      </li>
                      <li class="flex justify-start items-center gap-2 rounded-full py-3 px-6 bg-red-500 text-white cursor-pointer" @click="showRecordingOptions()" >
                           <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M15 10l4.553-2.276A1 1 0 0121 8.618v6.764a1 1 0 01-1.447.894L15 14M5 18h8a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
                          </svg>
                           <span>Start Recording</span>
                      </li>
                 </ul>
            </div>
       </section>
       <section >
            <div id="defaultModal" tabindex="-1" class="overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 w-full md:inset-0 h-modal md:h-full backdrop-opacity-90  bg-black/40 flex justify-center items-center" v-if="data.showModal">
          <div class="relative p-4 w-full max-w-lg h-full md:h-auto">
             <!-- Modal content -->
             <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
                 <!-- Modal header -->
                 <div class="flex justify-between items-center p-5 rounded-t border-b dark:border-gray-600">
                     <h3 class="text-xl font-medium text-gray-900 dark:text-white">
                         New Recording
                     </h3>
                     <button type="button" class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm p-1.5 ml-auto inline-flex items-center dark:hover:bg-gray-600 dark:hover:text-white" data-modal-toggle="defaultModal" @click="closeModal()">
                         <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>  
                     </button>
                 </div>
                 <!-- Modal body -->
                 <div class="p-6 space-y-6 w-full mx-auto px-6">
                     <label for="my-projects">Save the recording in</label>
                     <select id="my-projects" name="my-projects" v-model="data.chosenProject" class="block bg-gray-100 py-3 rounded-lg px-3 my-2 mx-auto w-full">
                          <option disbaled value="">Select a project</option>
                          <option v-for="project in data.projects" :key="project.id" :value="project.name">{{project.name}}</option>
                     </select>
                     
                 </div>
                 <ul class='w-10/12 mx-auto py-3'>
                      <li class="flex justify-between items-center">
                           <p class="font-bold text-sm tracking-wide text-gray-600 ">Record screen</p>
                           <label for="default-toggle" class="inline-flex relative items-center cursor-pointer">
                                <div>
                                     <input type="checkbox" value="" id="default-toggle" class="sr-only peer" :checked="data.recordingOptions.screen" >
                                     <div class="w-11 h-6 bg-gray-300 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-green-300 dark:peer-focus:ring-green-800 rounded-full peer dark:bg-gray-700 peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600 peer-checked:bg-green-600"></div>
                                </div>
                                
                         </label>
                      </li>
                      <li class="flex justify-between items-center my-6">
                           <p class="font-bold text-sm tracking-wide text-gray-600">Record Camera</p>
                           <label for="default-toggle-2" class="inline-flex relative items-center cursor-pointer">
                                <div>
                                     <input type="checkbox" value="" id="default-toggle-2" class="sr-only peer" :checked="data.recordingOptions.video" >
                                     <div class="w-11 h-6 bg-gray-300 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-green-300 dark:peer-focus:ring-green-800 rounded-full peer dark:bg-gray-700 peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600 peer-checked:bg-green-600"></div>
                                </div>
                                
                         </label>
                      </li>
                      <li class="flex justify-between items-center">
                           <p class="font-bold text-sm tracking-wide text-gray-600 ">Record Mic</p>
                           <label for="default-toggle-3" class="inline-flex relative items-center cursor-pointer">
                                <div>
                                     <input type="checkbox" value="" id="default-toggle-3" class="sr-only peer" :checked="data.recordingOptions.audio">
                                     <div class="w-11 h-6 bg-gray-300 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-green-300 dark:peer-focus:ring-green-800 rounded-full peer dark:bg-gray-700 peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all dark:border-gray-600 peer-checked:bg-green-600"></div>
                                </div>
                                
                         </label>
                      </li>
                 </ul>
                 <!-- Modal footer -->
                 <div class="flex justify-center items-center p-6 space-x-2 rounded-b border-t border-gray-200 dark:border-gray-600">
                     <button type="button" class="text-white bg-blue-400 hover:bg-blue-800 focus:ring-4 focus:outline-none rounded-full focus:ring-blue-300 font-medium text-sm px-12 py-2.5 text-center " @click="startRecording()">Start Recording</button>
                 </div>
             </div>
          </div>
          </div>
       </section>
</template>

<style>

</style>
