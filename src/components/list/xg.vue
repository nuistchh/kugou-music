<template>
  <div class="kugou-xg">
    <img src="./banner.jpg" alt="">
    <div class="kugou-xg-list">
      <ul>
        <li v-for="item in $store.state.xgList"  :hash = item.hash @click="getUrl">
          {{item.filename}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

    export default {
        name:'list',
        data(){
          return {

          }
        },
        methods:{
          getUrl(e){
            this.$store.state.searchFlag = false;
        	this.$store.state.currentList = this.$store.state.xgList;
            //歌曲信息
            this.$store.state.getMusic.hash = e.target.getAttribute('hash');
            this.$store.state.getMusic.name = e.target.innerHTML.replace(/(^\s*)|(\s*$)/g, "");
            this.$store.commit('getApi')
            this.$store.state.next.hash = e.target.nextSibling.getAttribute('hash');
            this.$store.state.next.name = e.target.nextSibling.innerHTML;
          }
        },
        mounted(){
     	 	this.$http.get('/api/?json=true',{
      						}).then(function(response){
        	var data = response.body;
       		this.data = data;
       		this.$store.state.xgList = data.data;
        	 
     		});
    	}
        
    }
</script>

<style>
  .kugou-xg{
    margin-top: 6.4286rem;
    margin-bottom:4.2143rem;
  }
  .kugou-xg img{
    width: 100%;
  }
  .kugou-xg ul{
    padding: 0 10px;
  }
  .kugou-xg ul li{
    width: 100%;
    font-family: 'Microsoft Yahei';
    border-bottom: 1px solid #eee;
    font-size: 1rem;
    padding: 20px 0;
  }
</style>
