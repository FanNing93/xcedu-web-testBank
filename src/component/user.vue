<template>
  <div class="app-testBank-header-btns">
    <el-avatar v-if="user.avatar" :src="avatarUrl" size="medium" />
    <el-avatar v-else size="medium" class="bgcolor"> {{ user.name && user.name.slice(-2) || '' }} </el-avatar>
    <!-- <i class="icon icon-home color" /> -->
    <!-- <i class="icon icon-logout color" /> -->
  </div>
</template>
<script>
import { getUserInfo } from '@/api/index'
export default {
  data () {
    return {
      user: ''
    }
  },
  computed: {
    avatarUrl: function () {
      var href = window.location.href
      var spstr = '//'
      var prefix = href.indexOf(spstr) + spstr.length
      var aim = href.substring(prefix)
      var url = href.substring(0, prefix) + aim.substring(0, aim.indexOf('/'))
      return url + '/api/v1/' + this.user.avatar + '&access_token=' + localStorage.getItem('token')
    }
  },
  mounted () {
    getUserInfo().then(res => {
      this.user = res
      window.localStorage.setItem('user', JSON.stringify(this.user))
    })
  }
}
</script>
