<template>
  <div class="flex flex-col items-center space-y-0.5 font-monsterrat bg-gradient-to-r from-blue-800 to-cyan-500 p-8">
    <div class="font-semibold text-xl text-white font-montserrat uppercase">
      SRM Institute of Science & Technology (Tiruchirapalli Campus)
    </div>
    <div class="font-montserrat font-bold text-2xl text-white uppercase">
      Department of Computer Science & Engineering
    </div>
    <div class="text-white">Proudly Welcomes You All To</div>
    <div
      class="font-montserrat font-bold text-yellow-200 transition transform duration-500 ease-in-out hover:scale-110 text-2xl">
      21 Days Online International Faculty Development Program on
    </div>
    <div class="font-black uppercase text-lg tracking-wider text-yellow-200">Data Science Tools</div>
    <div class="text-white font-montserrat font-semibold text-2xl">12/07/2023 - 01/08/2023</div>
  </div>
  <div class="p-4 h-screen relative overflow-hidden" @touchmove="movedarotouch" @mousemove="movedaro">
    <div class="w-full">
      <div class="mx-auto flex flex-col items-center justify-center">
        <div class="p-2 flex flex-col items-center text-center">
          <HomePage />
        </div>
        <div v-for="light in lights" :key="light.name" class="w-full">
          <img :class="`absolute z-40 top-0
          ${buttons[light.name]
              ? 'block'
              : 'hidden'
            }`" :style="{ 'top': `${light.y + 30}px`, 'left': `${light.x + 20}px`, 'width': '50px', 'height': '50px' }"
            :src="`/brighterflame/${images[light.name]}.png`" />
          <button class="absolute bg-white border-red-700 border rounded-full z-30"
            :style="{ 'top': `${light.y + 70}px`, 'left': `${light.x + 40}px`, 'width': '10px', 'height': '10px' }"
            @click="x => lightUp(light.name)"></button>
        </div>
        <img class="flex-shrink-0 absolute z-20" :style="{ 'width': '15.6rem', 'height': '40.5rem', 'top': '60px' }"
          src="/lamp_better_y.webp" />
        <img class="flex-shrink-0 absolute z-10" :style="{ 'width': '75rem', 'height': '45.5rem', 'top': '360px' }"
          src="/kolam_better-modified.webp" />
      </div>
      <img class="w-36 h-36 absolute pointer-events-none z-50" :src="`/bettermatch/${currentDaro}.png`"
        :style="{ 'top': yco - 40 + 'px', 'left': xco + 'px' }" />
    </div>
  </div>
</template>
 
<script>
export default {
  data() {
    return {
      lights: [],
      xco: 100,
      yco: 100,
      currentDaro: 3,
      buttons: {
        one: false,
        two: false,
        three: false,
        four: false,
        five: false,
      },
      images: {
        one: 3,
        two: 3,
        three: 3,
        four: 3,
        five: 3,
      },
    }
  },
  mounted() {
    this.refreshLights()
    window.addEventListener('resize', this.refreshLights)
    setInterval(this.changeDaro, 50)
  },
  methods: {
    refreshLights() {
      this.lights = [
        { x: document.body.scrollWidth / 2 - 100, y: 80, name: 'one' },
        { x: document.body.scrollWidth / 2 - 150, y: 130, name: 'two' },
        { x: document.body.scrollWidth / 2 + 60, y: 130, name: 'three' },
        { x: document.body.scrollWidth / 2 + 20, y: 80, name: 'four' },
        { x: document.body.scrollWidth / 2 - 60, y: 160, name: 'five' },
      ]
    },
    lightUp(num) {
      if (!this.buttons[num]) setInterval(() => this.changeButton(num), 50)
      this.buttons[num] = true
    },
    changeButton(num) {
      this.images[num] = this.images[num] === 5 ? 2 : this.images[num] + 1
    },
    changeButtons() {
      for (const i of [1, 2, 3, 4, 5]) {
        this.changeButton(i)
      }
    },

    movedaro(e) {
      this.xco = e.pageX - 100
      this.yco = e.pageY
      //      console.log({ x: this.xco, y: this.yco })
    },
    changeDaro() {
      if (Math.random() < 0.5)
        this.currentDaro = this.currentDaro === 5 ? 2 : this.currentDaro + 1
    },
    movedarotouch(e) {
      this.xco = e.touches[0].pageX
      this.yco = e.touches[0].pageY
    },
  },
}
</script>