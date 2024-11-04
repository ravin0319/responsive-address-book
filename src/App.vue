<template>
  <div id="app">
    <ContactList />
  </div>
</template>

<script>
import ContactList from './components/ContactList.vue';

export default {
  components: {
    ContactList
  }
};
</script>

<style lang="scss">
@import './assets/styles.scss';

#app {
  background-color: #eeeeee;
  min-height: 100vh;
  padding: 20px;
}
</style>
