<template>
  <div class="rs-header-board">
    <header>
      <div class="logo-div">
        <router-link to="/"><img src="../../assets/img/rs-full-logo.png" alt="logo"></router-link>
      </div>
      <rs-header-board-body></rs-header-board-body>
      <rs-header-board-setting></rs-header-board-setting>
    </header>
  </div>
</template>

<script>
import RsHeaderBoardBody from './RsHeaderBoard/RsHeaderBoardBody'
import RsHeaderBoardSetting from './RsHeaderBoard/RsHeaderBoardSetting'
export default {
  name: 'rs-header-board',
  components: {RsHeaderBoardSetting, RsHeaderBoardBody},
  computed: {
    headerStyle () {
      return {
        width: screen.width + 'px'
      }
    }
  }
}
</script>

<style>
  @import '../../assets/css/rs-header.css';
  header {
    position: relative;
    height: 60px;
    z-index: 2;
  }
</style>
