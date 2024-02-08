<template>
  <div class="w-full max-h-screen overflow-y-hidden">
    <div class="p-4 h-screen relative overflow-hidden" @touchmove="movedarotouch" @mousemove="movedaro">
      <div class="flex flex-col items-center space-y-0.5 font-monsterrat px-8 py-2 relative mt-16">
        <img src="/SRM_TRP.png" class="w-48" alt="SRM Trichy" />
        <div class="text-2xl text-sky-900 font-montserrat uppercase font-black">
          SRM Group of Institutions
        </div>
        <div class="font-bold uppercase text-lg tracking-wider text-sky-900">
          Tiruchirappalli</div>
        <div class="flex gap-1">
          <div class="text-red-900 font-semibold">Proudly Welcomes You All To The Inaugural Ceremony Of</div>
        </div>
        <img src="/SRM_Innov.webp" class="w-72 mx-auto" />
        <div class="text-green-900 font-montserrat font-semibold text-lg">08 - 02 - 2024</div>
      </div>
      <div class="w-full">
        <div class="mx-auto flex flex-col items-center justify-center">
          <div v-for="light in lights" :key="light.name" class="w-full">
            <img :class="`absolute z-40 top-0 flame
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
          <img class="flex-shrink-0 absolute z-20 left-0" :style="{ 'width': '15.6rem', 'height': '40.5rem', 'top': '50px' }"
            src="/lamp_better_y_center.webp" />
            <img class="flex-shrink-0 absolute z-20 right-0" :style="{ 'width': '15.6rem', 'height': '40.5rem', 'top': '50px' }"
            src="/lamp_better_y_center.webp" />

          <img class="flex-shrink-0 absolute z-10" :style="{ 'width': '75rem', 'height': '45.5rem', 'top': '350px', left: '-480px' }"
            src="/kolam_better-modified.webp" />
            <img class="flex-shrink-0 absolute z-10" :style="{ 'width': '75rem', 'height': '45.5rem', 'top': '350px', right: '-480px' }"
            src="/kolam_better-modified.webp" />
        </div>
        <img class="w-36 h-36 fixed pointer-events-none z-50 text-center" :src="`/bettermatch/${currentDaro}.png`"
          :style="{ 'top': yco - 10 + 'px', 'left': xco + 'px' }" />
      </div>
    </div>
  </div>
</template>
 
<style scoped>
.flame {
  filter: drop-shadow(0 0 3rem #ff0000) drop-shadow(0 0 2rem #ff0000) drop-shadow(0 0 1rem #ff0000) drop-shadow(0 0 1rem #ff0000);
}
</style>

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
        { x: 130, y: 70, name: 'one' },
        { x: 160, y: 120, name: 'two' },
        { x: -20, y: 120, name: 'three' },
        { x: 20, y: 70, name: 'four' },
        { x: 65, y: 150, name: 'five' },
        { x: document.body.scrollWidth - 100 - 130, y: 70, name: 'six' },
        { x: document.body.scrollWidth - 100 - 160, y: 120, name: 'seven' },
        { x: document.body.scrollWidth - 100 + 20, y: 120, name: 'eight' },
        { x: document.body.scrollWidth - 100 - 20, y: 70, name: 'nine' },
        { x: document.body.scrollWidth - 190, y: 150, name: 'ten' },
      ]
    },
    lightUp(num) {
      if (!this.buttons[num]) setInterval(() => this.changeButton(num), 50)
      this.images[num] = 1
      this.buttons[num] = true
    },
    changeButton(num) {
      this.images[num] = this.images[num] === 5 ? 2 : this.images[num] + 1
    },
    changeButtons() {
      for (const i of [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]) {
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