<template>
  <div class="error">
    <div class="error-flex">
      <div class="left">
        <div class="left-item">
          <div class="left-item-animation left-item-num">401</div>
          <div class="left-item-animation left-item-title">您未被授权，没有操作权限~</div>
          <div class="left-item-animation left-item-msg">联系方式：1105290566@qq.com</div>
          <div class="left-item-animation left-item-btn">
            <el-button type="primary" round @click="onSetAuth">重新授权</el-button>
          </div>
        </div>
      </div>
      <div class="right">
        <img src="https://gitee.com/lyt-top/vue-admin-wonderful-images/raw/master/images/error/401.png" />
      </div>
    </div>
  </div>
</template>

<script>
import { clearSession } from "@/utils/storage";
import { resetRouter } from '@/router'
export default {
  name: "noAuth",
  methods: {
    // 重新授权
    onSetAuth() {
      clearSession();
      this.$store.commit('setMenuData', {})
      resetRouter() // 重置路由
      this.$router.push('/login')
    },
  },
};
</script>

<style scoped lang="scss">
.error {
  height: 100%;
  width: 900px;
  margin: auto;
  background-color: white;
  display: flex;
  .error-flex {
    width: 100%;
    margin: auto;
    display: flex;
    .left {
      flex: 1;
      height: 350px;
      position: relative;
      .left-item {
        position: absolute;
        top: 50%;
        left: 0;
        transform: translate(0%, -50%);
        .left-item-animation {
          opacity: 0;
          animation-name: error-num;
          animation-duration: 0.5s;
          animation-fill-mode: forwards;
        }
        .left-item-num {
          color: #d6e0f6;
          font-size: 55px;
        }
        .left-item-title {
          font-size: 20px;
          color: #333333;
          margin: 15px 0 5px 0;
          animation-delay: 0.1s;
        }
        .left-item-msg {
          color: #c0bebe;
          font-size: 12px;
          margin-bottom: 30px;
          animation-delay: 0.2s;
        }
        .left-item-btn {
          animation-delay: 0.2s;
        }
      }
    }
    .right {
      flex: 1;
      opacity: 0;
      animation-name: error-img;
      animation-duration: 2s;
      animation-fill-mode: forwards;
      img {
        width: 100%;
        height: 350px;
      }
    }
  }
  @keyframes error-num {
    0% {
      transform: translateY(60px);
      opacity: 0;
    }
    100% {
      transform: translateY(0);
      opacity: 1;
    }
  }
  @keyframes error-img {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
}
</style>