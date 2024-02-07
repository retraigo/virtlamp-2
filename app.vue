<template>
  <div class="w-full max-h-screen overflow-y-hidden">
    <div
      class="flex flex-col items-center space-y-0.5 font-monsterrat px-8 py-2 relative">
      <img src="/SRM_TRP.png" class="w-48 mx-auto" alt="SRM Trichy" />
      <div class="text-xl text-sky-900 font-montserrat uppercase font-black">
        SRM Group of Institutions
      </div>
      <div class="font-bold uppercase text-lg tracking-wider text-sky-900">
        Tiruchirappalli</div>
      <div class="text-black">Proudly Welcomes You All To</div>
      <div class="text-black font-semibold">The Inaugural Ceremony Of</div>
      <img src="/SRM_Innov.png" class="w-72 mx-auto" />
      <div class="font-black uppercase text-lg tracking-wider text-sky-900 font-serif font-bold">Innovate for Progress, Build for Tomorrow!</div>
      <div class="text-black font-montserrat font-semibold text-lg">08/02/2024</div>
    </div>
    <div class="p-4 h-screen relative overflow-hidden" @touchmove="movedarotouch" @mousemove="movedaro">
      <div class="w-full">
        <div class="mx-auto flex flex-col items-center justify-center">
          <div v-for="light in lights" :key="light.name" class="w-full">
            <img :class="`absolute z-40 top-0
          ${buttons[light.name]
                ? 'block'
                : 'hidden'
              }`"
              :style="{ 'top': `${light.y + 50}px`, 'left': `${light.x + 30}px`, 'width': '30px', 'height': '30px' }"
              :src="`/brighterflame/${images[light.name]}.png`" />
            <button :class="`${buttons[light.name]
              ? 'hidden'
              : 'block'
              } absolute bg-white border-red-700 border rounded-full z-30`"
              :style="{ 'top': `${light.y + 70}px`, 'left': `${light.x + 40}px`, 'width': '10px', 'height': '10px' }"
              @click="x => lightUp(light.name)"></button>
          </div>
          <img class="flex-shrink-0 absolute z-20" :style="{ 'width': '15.6rem', 'height': '40.5rem', 'top': '0px' }"
            src="/lamp_better_y.webp" />
          <img class="flex-shrink-0 absolute z-10" :style="{ 'width': '75rem', 'height': '45.5rem', 'top': '300px' }"
            src="/kolam_better-modified.webp" />
        </div>
        <img class="w-36 h-36 fixed pointer-events-none z-50 text-center" :src="`/bettermatch/${currentDaro}.png`"
          :style="{ 'top': yco - 10 + 'px', 'left': xco + 'px' }" />
      </div>
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
        { x: document.body.scrollWidth / 2 - 100, y: 20, name: 'one' },
        { x: document.body.scrollWidth / 2 - 150, y: 70, name: 'two' },
        { x: document.body.scrollWidth / 2 + 60, y: 70, name: 'three' },
        { x: document.body.scrollWidth / 2 + 20, y: 20, name: 'four' },
        { x: document.body.scrollWidth / 2 - 60, y: 100, name: 'five' },
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