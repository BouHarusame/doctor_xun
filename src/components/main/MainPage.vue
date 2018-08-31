<template>
  <div class="main">
    <div class="main_header clearfix">
      <div class="logo fl">
        <img src="./img/logo.jpg" alt="logo">
        <span >箱博士</span>
      </div>
      <div class="login fr">
        <router-link to="/login" class="signIn" v-if="!isLogin">登录</router-link>
        <div class="uerInfo" v-else>
          <span>欢迎回来 !</span>
          <span class="avatar">
            <img src="./img/avatar.png" alt="头像">
          </span>
          <div class="uerName">
            <p>{{uerInfo.mobile}}</p>
            <router-link to="" class="enter">进入单证中心</router-link>
          </div>
        </div>
        <div class="languge">
          <el-dropdown trigger="click" class="lan_d" @command="handleChange">
            <span class="el-dropdown-link" >
              {{currentLanguge}}<i class="el-icon-arrow-down el-icon--right"></i>
            </span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item command="中文">中文</el-dropdown-item>
              <el-dropdown-item command="English">English</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
        <div class="signUp" v-if="isLogin">
          <img src="./img/sign-out.png" alt="退出登录">
          <span>退出</span>
        </div>
      </div>
    </div>
    <div class="main_banner">
      <img src="https://www.anycase.cn//data/static/home/banner.png?_t=2018062001" alt="">
    </div>
    <div class="main_content">
      <div class="main_title">
        <img src="" alt="">
        <h4></h4>
        <p></p>
      </div>
      <div class="content_01">
        
      </div>
    </div>
  </div> 
</template>
<script>
export default {
  name: 'mainPage',
  data () {
    return {
      isLogin: false,
      currentLanguge: '中文',
      uerInfo: {
        mobile: '13956927665'
      }
    }
  },
  created () {
    console.log(localStorage.languge)
    this.currentLanguge = localStorage.languge === undefined ? this.$i18n.locale : localStorage.languge
  },
  methods: {
    handleChange (languge) {
      if (this.$i18n.locale === languge) return
      this.$confirm('是否切换当前语言？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning',
        center: true
      }).then(() => {
        this.$i18n.locale = languge
        localStorage.setItem('lang', languge)
        this.currentLanguge = this.$i18n.locale
      }).catch(() => {

      })
    }
  }
}
</script>
<style lang="stylus">
  .main
    font-family "微软雅黑"
    font-size 14px
    width 100%
    min-width 1200px
    .main_header
      position relative
      height 100px
      line-height 100px
      box-sizing border-box
      padding 0 60px 0 46px
      background rgba(255,255,255,1)
      box-shadow 0px 6px 17px 1px rgba(59,127,225,0.44)
      .logo
        width 304px
        img
          width 105px
          height 65px
          display inline-block
          vertical-align middle
        span
          font-size 48px
          font-family fzzyjt
          color #0456DE
          vertical-align middle
          margin-left 7px
          height 65px
          line-height 65px
      .signIn
          width 118px
          height 40px
          background  #0456DE
          border-radius 20px
          display inline-block
          vertical-align middle
          font-size 18px
          color #ffffff
          line-height 40px
          margin-right 30px
        .uerInfo
          display inline-block
          font-size 14px
          color #222
          margin-right 20px
          span
            display inline-block
            vertical-align middle
            margin-right 15px
          .avatar
            width 40px
            height 40px
            padding 5px
            border 1px solid #0456DE
            border-radius 50%
            overflow hidden
            margin 0 5px
            img
              width 40px
              height 40px
              vertical-align top
          .uerName
            display inline-block
            line-height 1.8
            vertical-align middle
            .enter
              color #0d5ee7
        .languge
          display inline-block
          width 70px
          .lan_d
            line-height 1
            font-weight bold
            color #0456DE
        .signUp
          display inline-block
          img, span
            display inline-block
            vertical-align middle
    .main_banner
      width 100%
      height auto
      img
        width 100%
        height auto
    
</style>
