<template></template>
<script>
export default {
  mounted() {
    let routeQuery = sessionStorage.getItem('reloadThemeRoute')
    if (routeQuery) {
      this.$router.push(routeQuery)
      sessionStorage.removeItem('reloadThemeRoute')
    }
    else {
      this.$router.push('/')
    }
  }
}
</script>