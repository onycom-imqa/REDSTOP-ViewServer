<template>
  <div class="rs-tb-nav">
    <nav>
      <rs-tb-nav-header :init-nav-header-list="navHeaderList" @headerSelectedEvent="headerSelected"></rs-tb-nav-header>
      <rs-tb-nav-body v-if="headerKey===0" :init-tree-data="this.$store.state.app.treeData" :init-header-key="key"></rs-tb-nav-body>
      <rs-tb-nav-body2 v-else-if="headerKey===1" :init-tree-data="this.$store.state.app.treeData" :init-header-key="key"></rs-tb-nav-body2>
      <!--<span>{{this.$store.state.app.treeData}}</span>-->
      <div class="importButton">
        <button id="i-button" @click="showModal = true" style="text-align: center">Import APIs from Swagger</button>
      </div>
      <rs-import-modal v-if="showModal" @close="showModal = false"></rs-import-modal>
    </nav>
  </div>
</template>

<script>
/* eslint-disable vue/no-dupe-keys */
/* eslint-disable */
  import RsImportModal from './RsImport/RsImportModal'
  import RsTbNavHeader from './RsTbNav/RsTbNavHeader'
  import RsTbNavBody from './RsTbNav/RsTbNavBody'
  import RsTbNavBody2 from './RsTbNav/RsTbNavBody2'

  export default {
    name: 'rs-tb-nav',
    components: {RsTbNavBody, RsTbNavHeader, RsImportModal, RsTbNavBody2},
    computed: {
      navStyle() {
        return {
          width: screen.width * 0.2 + 'px'
        }
      }
    },
    data() {
      return {
        headerKey: 0,
        navHeaderList: ['Explorer', 'History'],
        windowWidth: window.innerWidth,
        showModal: false
      }
    },
    methods: {
      handleWindowResize(event) {
        this.windowWidth = event.currentTarget.innerWidth
        this.navStyle()
      },
      navStyle() {
        return {
          width: screen.width * 0.2 + 'px'
        }
      },
      headerSelected(key) {
        this.headerKey = key
      }
    },
    beforeDestroy: function () {
      window.removeEventListener('resize', this.handleWindowResize)
    },
    mounted() {
      window.addEventListener('resize', this.handleWindowResize)
    }
  }
</script>

<style scoped>
  nav {
    position: absolute;
    top: 50px;
    left: 0;
    width: 20%;
    height: 100%;
    background-color: #ffffff;
    border-right: 1px solid #F2F7FB;
  }

  #i-button {
    width: 150%;
    height: 43px;
    border-radius: 20px;
    box-shadow: 0 2px 4px 0 #c6d5e9;
    background-color: #39496d;
    color: white;
    font-family: TitilliumWeb;
    font-size: 14px;
    font-weight: bold;
  }
  .importButton{
    position: absolute;
    right: 10%;
    left: 10%;
    display:flex;
    align-items:center;
    justify-content:center;
    bottom: 8%;
  }
</style>
