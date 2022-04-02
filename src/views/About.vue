<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="test">test</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      
    }
  },
  methods: {
    test() {
      this.$swal('Any fool can use a computer')
    }
  },
}
</script>
