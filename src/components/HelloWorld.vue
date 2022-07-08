<script setup>
import { ref , reactive, watchEffect } from 'vue'
import DashboardHeader from './DashboardHeader.vue'

const data = reactive({
     totalNumber: 25,
     recordings: [
          {image: "http://localhost:3000/src/assets/forgot.jpg", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "1 month ago", id: 1},
          {image: "http://localhost:3000/src/assets/easy.jpg", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "2 month ago", id: 2},
          {image: "http://localhost:3000/src/assets/settings.jpg", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "1 week ago", id: 23},
          {image: "https://i.pravatar.cc/150?img=9", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "2 weeks ago", id: 24},
          // {image: "https://i.pravatar.cc/150?img=10", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "1 month ago", id: 54},
          // {image: "https://i.pravatar.cc/150?img=20", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "4 month ago", id: 12},
          // {image: "https://i.pravatar.cc/150?img=67", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "3 weeks ago", id: 13},
          // {image: "https://i.pravatar.cc/150?img=12", title: "The title which is usualy longer than this and can be annoying", views: 30, size: "1002 kb", last_modified: "1 month ago", id: 15}
     ],
     screens: {controls: true, filledLibrary: true, video: false, stream: {}}
})
 const count = ref(0)
 const video = ref(null)
 const user = {
     name: 'Cody Fisher',
     email: 'codyfisher@gmail.com'
 }
 watchEffect(() => {
  if (video.value) {
    console.log("Now available")
    video.value.srcObject = data.screens.stream
    video.onloadedmetadata = function(e) {
       video.play();
    };
  } else {
    console.log("not available")
  }
})

 function recordingStarted(value)
 {
      data.screens.filledLibrary = false
      data.screens.stream = value
      data.screens.video = true
      
 }
</script>
 <template>
      <main class="bg-white relative py-0 min-h-min relative" v-if="data.screens.filledLibrary">
          <header class="flex justify-around items-center border-b-2 border-gray-200  sticky-0">
               <div class="flex justify-start items-center gap-3 py-6">
                    <div class="outer-circle w-8 h-8 rounded-xl flex justify-center items-center">
                         <div class="inner-circle h-5 w-5 rounded-full bg-white"></div>
                    </div>
                    <h1 class="header font-bold text-2xl inline ">Adilo</h1>
               </div>
               <nav class="flex justify-start gap-10 text-gray-800">
                    <li class="py-6"><a>Projects</a></li>
                    <li class="py-6 relative"><a>Tools and App </a> <span class="text-xl  mx-3 absolute top-4">&#8964;</span></li>
                    <li class="py-6"><a>Channels</a></li>
                    <li class="py-6"><a>Contacts</a></li>
                    <li class="py-6"><a>Analytics</a></li>
                    <li class="py-6"><a>Settings</a></li>
               </nav>
               <div class="flex justify-start gap-4 items-center">
                    <p class="font-bold border-r-2 border-gray-200 px-2 cursor-pointer">Help</p>
                    <div class="flex justify-start gap-3">
                         <img src="https://i.pravatar.cc/150?img=1" alt="user avatar" class="w-12 h-12 rounded-xl cursor-pointer w-12 h-12 ">
                         <div>
                              <h3 class="text-left font-bold">{{user.name}}</h3>
                              <p>{{user.email}}</p>
                         </div>
                    </div>
               </div>
          </header>
          <div class="flex justify-start items-start my-0 h-screen" >
               <section class="bg-blue-100 w-2/12 py-5 border-r-2 border-gray-400 h-full sticky">
                    <ul class="h-full">
                         <li class="flex justify-start ml-3 py-3 px-3 gap-8 cursor-pointer hover:bg-gray-100 rounded-lg mx-2 hover:shadow-sm">
                              <img src="../assets/video-player.svg" alt="video player icon" class="w-5 h-5"/>
                              <span class="text-md">My Recordings</span>
                         </li>
                         <li class="flex justify-start ml-3 py-3 px-3 gap-8 cursor-pointer hover:bg-gray-100 rounded-lg mx-2 hover:shadow-sm">
                              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                   <path stroke-linecap="round" stroke-linejoin="round" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z" />
                              </svg>
                              <span>Requested</span>
                         </li>
                    </ul>
               </section>
               <section class="w-full">
                    <DashboardHeader :combined='data.totalNumber' v-if="data.screens.controls" @recording="recordingStarted"/>
                    <div>
                         <div class="relative overflow-x-auto shadow-md sm:rounded-lg mx-8 my-12">
                         <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                            <thead class="text-xs uppercase dark:bg-gray-700 dark:text-gray-400">
                                <tr>
                                    <th scope="col" class="px-6 py-3">
                                        Recordings
                                    </th>
                                    <th scope="col" class="px-6 py-3">
                                        Title
                                    </th>
                                    <th scope="col" class="px-6 py-3">
                                        Views
                                    </th>
                                    <th scope="col" class="px-6 py-3">
                                        Size
                                    </th>
                                    <th scope="col" class="px-6 py-3">
                                        Last modified
                                    </th>
                                    <th scope="col" class="px-6 py-3">
                                        <span class="sr-only"></span>
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr class="bg-white " v-for="recording in data.recordings" :key="recording.id">
                                    <th scope="row" class="px-2 py-4 font-medium text-gray-900 dark:text-white whitespace-nowrap">
                                        <img :src="recording.image" class="w-48 h-24 rounded my-2 cursor-pointer"/>
                                    </th>
                                    <td class="px-3 py-4">
                                        {{recording.title}}
                                    </td>
                                    <td class="px-6 py-4">
                                        {{recording.views}}
                                    </td>
                                    <td class="px-6 py-4">
                                        {{recording.size}}
                                    </td>
                                    <td class="px-6 py-4 text-right">
                                        {{recording.last_modified}}
                                    </td>
                                    <td class="px-6 py-4 text-right cursor-pointer">
                                         <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                             <path stroke-linecap="round" stroke-linejoin="round" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z" />
                                             </svg>
                                    </td>
                                </tr>
                            </tbody>
                         </table>
                         </div>
                    </div>
               </section>
          </div>
      </main>
      <aside v-if="!data.screens.filledLibrary" class="vid-container py-20 flex justify-center h-screen w-screen">
           <div class="my-4 w-6/12">
                <p class="text-left font-bold text-gray-700  mb-2 flex justify-start items-center"> 
                     <div class="border border-red-600 rounded-full mr-2 bg-white py-1 px-1">
                          <div class="w-2 h-2 bg-red-500 rounded-full py-1 px-1"></div>
                     </div>Live preview</p>
                <div class="vid-screen mx-auto w-full h-3/4 rounded-lg">
                     <video class="w-full h-full" ref="video" controls autoplay id="video" v-if="data.screens.video"></video>
                </div>
                <div class="flex justify-center items-center p-6 space-x-2 rounded-b border-t border-gray-200 dark:border-gray-600">
                    <button type="button" class="text-white bg-blue-400 hover:bg-blue-800 focus:ring-4 focus:outline-none rounded-full focus:ring-blue-300 font-medium text-sm px-12 py-3 text-center " @click="startRecording()">Stop Recording</button>
                </div>
           </div>
      </aside>
 </template>
<style scoped>
li{
     list-style: none;
     cursor: pointer;
}
.vid-container
{
     background-color: #EAFAFF;
}
.vid-screen
{
     background-color: #21455E;
}
.outer-circle
{
     background-color: #FBBD71
}
</style>
