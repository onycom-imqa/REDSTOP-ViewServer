<template>
  <div class="rs-tb-aside-title">
    <div width="80%" style="float: left;">
      <img v-if="currentBlock.type=='group'" class='title-icon' src="../../assets/img/group.png">
      <img v-else-if="currentBlock.type=='case'" class='title-icon' src="../../assets/img/case.png">
      <img v-else class='title-icon' src="../../assets/img/api.png">
      <span v-if="currentBlock.type=='api'"><b style="color: deepskyblue;">{{currentBlock.method}}</b>&nbsp;&nbsp;{{currentBlock.url}}&nbsp;</span>
      <span v-else>{{currentBlock.name}}</span>
      <img id="edit-icon" src="../../assets/img/edit.png" width="15" height="15">
    </div>
    <!--<div width="20%" style="float: right;">-->
    <!--<img id="play-icon" src="../../assets/img/play.png" width="35" height="35" @click="clickPlay">-->
    <!--</div>-->
    <br><br>
  </div>
</template>

<script>
/*eslint-disable */
  import casing from 'eslint-plugin-vue/lib/utils/casing'

  export default {
    props: ['initBlockId'],
    name: 'rs-tb-aside-title',
    watch: {
      initBlockId: function () {
        // console.log('여기는 rs-tb-aside-title watch')
        let treeDataSerial = this.$store.state.app.treeDataSerial
        let currentBlockID = this.$store.state.app.currentBlockId
        let currentBlock = null
        if (treeDataSerial !== null) {
          for (let atom of treeDataSerial) {
            if (atom.id === currentBlockID) {
              currentBlock = atom
              break;
            }
          }
          this.currentBlock = currentBlock
          // console.log(currentBlock)
        }
      }
    },
    created: function () {
      // console.log('여기는 rs-tb-aside-title created')
      let treeDataSerial = this.$store.state.app.treeDataSerial
      let currentBlockID = this.$store.state.app.currentBlockId
      let currentBlock = null
      if (treeDataSerial !== null) {
        for (let atom of treeDataSerial) {
          if (atom.id === currentBlockID) {
            currentBlock = atom
            break;
          }
        }
        this.currentBlock = currentBlock
        // console.log(currentBlock)
      }
    },
    data: function () {
      return {
        currentBlock: {id: 'default', name: 'default', parentBlockId: null, type: 'api'}
      }
    },
    methods: {
      clickPlay: function () { // 여기서 API 테스트 하기
        console.log('클릭 클릭 이벤트 탔습니다!')
        this.$http
          .get('http://localhost:3000/api')
          .then(response => {
            console.log(response)
          })
        // var param = {
        //   url: this.curUrl,
        //   method: this.curMethod,
        //   data: this.tableValue
        // }
        // 서버에 테스트 보내기 !!
        //
        // this.$http.post('http://localhost:3000/api').then((response) => {
        //   // this.$emit('apiTestResultEvent', response.data)// 받아온 데이터로 이벤트 트리거
        //   console.log('함수탓습니다!')
        //   console.log(response)
        // })
      }
    }
  }
</script>

<style scoped>
  .title-icon {
    padding-right: 10px;
  }
</style>
