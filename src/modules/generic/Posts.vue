<template>
  <div class="containers">
    <div class="row" style="width: 103%; margin-left: 0px;">
      <div class="column" style="margin-right: 10px;">
        <img :src="config.BACKEND_URL + data.account.profile.url" width="40px" height="40px" style="border-radius: 25px; margin-left: 2px;">
      </div>
      <div class="column" style=" width: 84%; margin-top: 4px; line-height: 15px;"> 
        <b>{{data.account.information.first_name ? data.account.information.first_name + ' ' + data.account.information.last_name : data.account.username}}</b>
        <p style="font-size: 12px;">{{data.created_at_human}}</p>
      </div>
      <div class="column" style="padding-right: 8px;">
      <span class="right-menu-icons">
      <div class="dropdown" >
        <span class="nav-item"  data-toggle="dropdown" v-on:click="makeActive('dropdown')" >
        <i class="fas fa-ellipsis-h"></i>
        <Dropdown/>
        </span>
      </div>
      </span>
    </div>
    </div>
    <div style="padding: 10px;">
      <p>{{data.text}}</p>
      <PostImage :images="data.images"/>
      <i class="fas fa-praying-hands praying-hands"></i>
      <span style=" margin-right: 50px; vertical-align: 2px;">Amen</span>
      <i class="fas fa-heart love"></i>
      <span style=" margin-right: 50px; vertical-align: 3px;">Love</span>
      <i class="fas fa-share share"></i>
      <span style=" margin-right: 50px; vertical-align: 3px;">Share</span>
    </div>
    <div style="width: 100%; margin-left: 0px; margin: 10px;" v-if="data.comment_replies && data.comment_replies.length > 0">
      <div class="row" style="margin-left: 15px;" v-for="(item, index) in data.comment_replies" :key="index">
        <div class="column" style="margin-right: 10px;">
          <img :src="require('src/assets/img/test.jpg')" width="40px" height="40px" style="border-radius: 25px;">
        </div>
        <div class="column" style="width: 82%; margin-top: 4px; line-height: 15px;">
          <b>{{item.account.information.first_name ? item.account.information.first_name + ' ' + item.account.information.last_name : item.account.username}}</b>
          <p style="font-size: 12px;">{{item.created_at}}</p>
        </div>
        <div class="column" style="width: 5%;">
          <span class="right-menu-icons">
          <div class="dropdown">
            <span class="nav-item" data-toggle="dropdown" v-on:click="makeActive('dropdown')" v-bind:onkeypress="makeActive('')">
            <i class="fas fa-ellipsis-h"></i>
            <Dropdown/>
            </span>
            </div>
          </span>
        </div>
        <p style="margin: 10px; margin-top: 10px;">{{item.text}}</p>
      </div>
    </div>
    <div style="width: 100%; margin-left: 0px; margin: 10px;">
      <input type="text" class="inputs" placeholder="Type here">
    </div>
  </div>
</template>
<script>
import AUTH from 'src/services/auth'
import CONFIG from 'src/config.js'
import Dropdown from 'src/modules/generic/Dropdown'
import PostImage from 'src/modules/generic/PostImage'
export default{
  props: ['data'],
  data(){
    return {
      user: AUTH.user,
      dropdown: 'dropdown-menu',
      config: CONFIG
    }
  },
  components: {
    Dropdown,
    PostImage
  },
  methods: {
    makeActive(icon){
      if(icon === 'dropdown-menu'){
        this.settingFlag = true
        this.menuFlag = true
        this.notifFlag = false
      }
    }
  }
}
</script>
<style scoped lang="scss">
@import "~assets/style/colors.scss";
.inputs{
  border-radius: 20px;
  height: 40px;
  border: .5px solid rgb(235, 235, 235);
  margin-top: 5px;
  outline: none;
  width: 95%;
  padding: 15px;
}
.love, .share, .praying-hands{
  font-size: 20px;
  color: $secondary;
}
.containers{
  width: 100%;
  background-color: white;
  padding: 10px;
  border-radius: 10px;
  border: .5px solid rgb(235, 235, 235);
  cursor: pointer;
}
</style>
