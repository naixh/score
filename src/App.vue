<template>
<div class="h-screen">
   <div class="bg-white-800 h-full">
      <div class="flex bg-red-300 flex-row h-1/2">
         <div class="grow w-9/12 bg-blue-800  place-items-center grid">
            <div class="align-middle items-center text-center">
               <p class=" text-9xl text-white"> FINAL SCORE </p>
               <br>
            </div>
         </div>
         <div class="grow-0 w-full bg-yellow-300 flex">
            <div class="grow w-1/2 h-full bg-blue-800   text-center grid place-content-evenly ">
               <div class="align-middle items-center text-center">
                  <textarea spellcheck="false" class=" w-full text-8xl align-bottom font-extrabold text-white bg-transparent text-center" >TEAM</textarea>
                  <input class="w-full align-middle text-white bg-transparent text-center font-extrabold " style="font-size: 13.75rem;" type="number">
               </div>
            </div>
            <div class="grow-0 w-1/2  bg-blue-800 text-center grid place-content-evenly">
               <div class="align-middle items-center text-center">
                   <textarea spellcheck="false" class=" w-full text-8xl align-bottom font-extrabold text-white bg-transparent text-center" >TEAM</textarea>
                   <input class="w-full align-middle text-white bg-transparent text-center font-extrabold " style="font-size: 13.75rem;" type="number">
               </div>
            </div>
         </div>
      </div>
      <div class="bg-red-800 h-1/2">
         <div class="flex bg-red-300 flex-row h-full">
            <div class="grow w-7/12 bg-gray-900  grid  border-r-8">
               <div class="align-middle text-center py-20">

                  <p class=" text-8xl align-top text-white"> Running Time </p>
                  <br>
                   <div id="counter" v-cloak>
                       <div v-if="time!==0">
                               <timer :time="time"></timer>
                           <div>
                               <button v-if="!isRunning" @click="start">Start</button>
                               <button v-if="isRunning" @click="stop">Stop</button>
                               <button @click="reset">Reset</button>
                           </div>
                       </div>
                       <form v-else >
                           <label for="min">Minutes<br />
                               <input type="number" class="bg-transparent text-4xl font-bold  text-center" v-model="min" name="time_m" id="min" min="0" max="59">
                           </label>
                           <br>
                           <button type="button" @click="sendTime">Set time</button>
                       </form>
                   </div>

               </div>
            </div>
            <div class="grow-0 w-full bg-gray-900">
               <div class="grow w-full h-4/6 bg-gray-200 flex">
                  <div class="grow w-1/3 h-full bg-gray-900 p-5  ">
                     <div class="bg-yellow-300 h-full rounded-lg text-center grid place-content-evenly">
                        <input type="number" class="bg-yellow-300 rounded-lg  text-9xl font-bold w-full text-center" style="font-size: 14rem;"  >
                     </div>
                  </div>
                  <div class="grow-0 w-1/2 h-full bg-gray-900 ">
                     <div class="bg-gray-900 h-full text-center grid place-content-evenly">
                        <span class="text-9xl font-bold text-white whitespace-normal  " >Period Score</span>
                     </div>
                  </div>
                  <div class="grow-0 w-1/3  bg-gray-900">
                     <div class="grow h-full bg-gray-900 p-5  ">
                        <div class="bg-yellow-300 h-full rounded-lg text-center grid place-content-evenly">
                            <input type="number" class="bg-yellow-300 rounded-lg  text-9xl font-bold w-full text-center" style="font-size: 14rem;"  >
                        </div>
                     </div>
                  </div>
               </div>
               <div class="grow-0 w-full  h-1/3 bg-gray-900 text-center ">
                  <div class="grow h-full w-5/12 bg-gray-900 float-left grid place-content-evenly pt-2">
                     <div class="bg-gray-900  h-full text-white">
                        <span class="text-6xl font-bold " >CATCH</span>
                        <input type="number" class="bg-gray-900 text-8xl font-bold w-full text-center" >
                     </div>
                  </div>
               </div>
            </div>
         </div>
      </div>
   </div>
   <div class="bg-blue-200 h-20 tes">
    <marquee ><input type="text" class="bg-transparent text-6xl font-bold w-full text-center" ></marquee>
   </div>
</div>

</template>
<script>


import HelloWorld from "./components/HelloWorld.vue";

export default {
    components: {
        'timer':HelloWorld
    },
data() {
    return {
        componentLoaded: false,
        isRunning: false,
        minutes: 10,
        secondes: 10,
        time:0,
        min: 0,
        sec: 0,
        timer: null,
        sound: new Audio("http://s1download-universal-soundbank.com/wav/nudge.wav")
    }
},


	methods: {
		 start () {
			 this.isRunning = true
			 if (!this.timer) {
				  this.timer = setInterval( () => {
						if (this.time > 0) {
							 this.time--
						} else {
							 clearInterval(this.timer)
							 this.sound.play()
							 this.reset()
						}
				  }, 1000 )
			 }
		 },

		 stop () {
			 this.isRunning = false
			 clearInterval(this.timer)
			 this.timer = null
		 },
		 reset () {
			  this.stop()
			  this.time = 0
			  this.secondes = 0
			  this.minutes = 0
		 },
        sendTime () {
            this.time = (this.min * 60 + this.secondes)
            this.time = this.prettify(this.time)
		 },


	},

}

</script>

