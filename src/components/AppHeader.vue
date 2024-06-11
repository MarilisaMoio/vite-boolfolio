<script>
    export default{
        name: 'AppHeader'
    }
</script>

<template>
    <header class="d-flex justify-content-center py-3">
      <ul class="nav nav-pills">
        <li class="nav-item"><router-link :to="{ name: 'home' }" class="nav-link">Home</router-link></li>
        <li class="nav-item"><router-link :to="{ name: 'projects' }" class="nav-link">Projects</router-link></li>
      </ul>
    </header>
</template>

<style scoped lang="scss">
    header{
        box-shadow: 0 0 5px rgb(2, 2, 73);
    }
</style>