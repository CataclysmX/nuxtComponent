<template lang="html">
  <div class="relative w-8 h-8">
    <input v-model="model" type="hidden">
    <div class="w-8 h-8 flex rounded bg-white hover:bg-gray-300 transition duration-200 group cursor-pointer" @click="checked = !checked">
      <div class="w-6 h-6 m-auto rounded transition duration-200 select-none" :class="[(selectedColor.defaultColor === '' ? 'bg-blue-500': selectedColor.defaultColor), (selectedColor.hoveredColor === '' ? 'group-hover:bg-blue-700' : 'group-hover:' + selectedColor.hoveredColor)]" />
    </div>
    <div class="absolute top-full overflow-hidden motion-safe:transition-all duration-500 select-none" :style="{maxHeight: checked ? ((colorClassList.length / 4) * 6) +'rem' : '0px'}">
      <div id="tooltips" class="bg-white w-32 relative my-4 rounded shadow-lg">
        <i />
        <div class="w-full flex flex-wrap">
          <div v-for="(item, key) in colorClassList" :key="key" class="w-1/4 my-2">
            <div class="w-6 h-6 m-auto rounded transition duration-200 cursor-pointer select-none border" :class="[item.defaultColor, 'hover:' + item.hoveredColor]" @click="colorParser(item)" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      checked: false,
      model: {
        defaultColor: '',
        hoveredColor: ''
      },
      selectedColor: {
        defaultColor: '',
        hoveredColor: ''
      },
      colorClassList: [
        {
          defaultColor: 'bg-blue-500',
          hoveredColor: 'bg-blue-700'
        },
        {
          defaultColor: 'bg-yellow-500',
          hoveredColor: 'bg-yellow-700'
        },
        {
          defaultColor: 'bg-red-500',
          hoveredColor: 'bg-red-700'
        },
        {
          defaultColor: 'bg-green-500',
          hoveredColor: 'bg-green-700'
        },
        {
          defaultColor: 'bg-indigo-500',
          hoveredColor: 'bg-indigo-700'
        },
        {
          defaultColor: 'bg-purple-500',
          hoveredColor: 'bg-purple-700'
        },
        {
          defaultColor: 'bg-pink-500',
          hoveredColor: 'bg-pink-700'
        },
        {
          defaultColor: 'bg-gray-500',
          hoveredColor: 'bg-gray-700'
        },
        {
          defaultColor: 'bg-white',
          hoveredColor: 'bg-white'
        }
      ]
    }
  },
  watch: {
    selectedColor () {
      this.$emit('input', this.model)
    }
  },
  methods: {
    colorParser (color) {
      const objColor = {
        color: color.defaultColor.match(/-([a-zA-Z0-9]+)/gmi)[0].replace(/-/gmi, ''),
        class: color.defaultColor.replace(/^[a-zA-Z]+-/gmi, ''),
        lightestCode: /-([0-9]+)/gmi.test(color.defaultColor) ? color.defaultColor.match(/-([0-9]+)/gmi)[0].replace(/-/gmi, '') : null
      }

      this.selectedColor = {
        defaultColor: color.defaultColor,
        hoveredColor: color.hoveredColor
      }
      this.model = objColor
    }
  }
}
</script>

<style lang="css" scoped>
#tooltips > i::after {
  content: " ";
  position: absolute;
  bottom: 100%;
  left: 12%;
  margin-left: -10px;
  border-width: 10px;
  border-style: solid;
  border-color: transparent transparent white transparent;
}
</style>
