<template>
  <div class="login-container">
    <!-- 导航栏 -->
    <van-nav-bar class="app-nav-bar" title="登录" left-arrow @click-left="$router.back()" />
    <!-- /导航栏 -->

    <!-- 登录表单 -->
    <van-cell-group>
      <van-field v-model="user.mobile" required clearable icon-prefix="toutiao" left-icon="shouji" label="手机号"
        placeholder="请输入手机号" />
      <van-field v-model="user.code" clearable icon-prefix="toutiao" left-icon="yanzhengma" label="验证码" placeholder="请输入验证码">
        <template #button>
          <van-button class="send-btn" size="mini" round>发送验证码</van-button>
        </template>
      </van-field>
    </van-cell-group>
    <div class="login-btn-wrap">
      <van-button class="login-btn" type="info" block @click="onLogin">登录</van-button>
    </div>
    <!-- /登录表单 -->
  </div>
</template>

<script>
export default {
  name: 'LoginIndex',
  components: {},
  props: {},
  data () {
    return {
      user: {
        mobile: '', // 手机号
        code: '' // 验证码
      }
    }
  },
  computed: {},
  watch: {},
  created () {},
  mounted () {},
  methods: {
    onLogin () {
      this.$toast.loading({
        message: '登录中...', // 提示文本
        forbidClick: true, // 禁止背景点击
        duration: 0 // 展示时长(ms)，值为 0 时，toast 不会消失
      })
      try {
        this.$toast.success('登录成功')
        this.$store.commit('setUser', this.user.mobile)
        this.$router.push('/my')
      } catch (err) {
        console.log(err)
        this.$toast.fail('登录失败，手机号或验证码错误')
      }
    }
  }
}
</script>

<style scoped lang="less">
  .login-container {
    .send-btn {
      width: 76px;
      height: 23px;
      background-color: #ededed;

      .van-button__text {
        font-size: 11px;
        color: #666666;
      }
    }

    .login-btn-wrap {
      padding: 26px 16px;

      .login-btn {
        background-color: #6db4fb;
        border: none;

        .van-button__text {
          font-size: 15px;
        }
      }
    }
  }
</style>
