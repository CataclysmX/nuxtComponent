<template>
  <div class="bg-gray-700 h-screen">
    <div class="container mx-auto flex flex-wrap py-4 ">
      <div class="w-1/4 border rounded p-4 border-gray-800 shadow">
        <label class="text-white" for="">color palette : </label>
        <colorPalette
          v-model="colorPalette"
          class="mx-auto"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      colorPalette: {}
    }
  }
}
</script>
