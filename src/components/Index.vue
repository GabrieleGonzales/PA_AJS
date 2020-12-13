<template>
  <div><br>
    <h2><img src='../icons/igti.png' width="50%"></h2>
  </div>
</template>

<script>
export default {
  data() {
    return {
      property: 'Example property.'
    }
  },

  computed: {
    propertyComputed() {
      return this.property
    }
  },
  created() {
  }
}
</script>