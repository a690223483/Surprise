<template>
  <div class="page">
    <div class="page__bd">
      <div class="userinfo" v-if="userInfo.nickName">
        <img class="userinfo-avatar" :src="userInfo.avatarUrl" />
        <p>{{userInfo.nickName}}</p>
      </div>
      <button
        class="userinfo-avatar"
        v-if="!userInfo.nickName"
        open-type="getUserInfo"
        @getuserinfo="authSetUser"
      >
        <div v-if="!userInfo.nickName">
          <img class="userinfo-avatar" src="/static/images/user.png" />
        </div>
      </button>

      <div class="weui-grids">
        <block v-for="(item,index) in grids" :key="index">
          <navigator url class="weui-grid" hover-class="weui-grid_active">
            <image class="weui-grid__icon" :src="item.src" />
            <div class="weui-grid__label">{{item.name}}</div>
          </navigator>
        </block>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userInfo: {},
      grids: [
        { src: "/static/images/user.png", name: "Button" },
        { src: "/static/images/user.png", name: "Cell" },
        { src: "/static/images/user.png", name: "Toast" }
      ]
    };
  },
  created() {
    this.getUserInfo();
  },

  methods: {
    authSetUser(e) {
      this.userInfo = e.mp.detail.userInfo;
    },
    getUserInfo() {
      // 调用登录接口
      var _this = this;
      wx.getUserInfo({
        //当已授权getUserInfo时
        success(res) {
          _this.userInfo = res.userInfo;
        },
        fail(err) {}
      });
    }
  }
};
</script>

<style>
.page {
  margin-top: 50px;
}
.userinfo {
  display: flex;
}
.userinfo-avatar {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  overflow: hidden;
  width: 160rpx;
  height: 160rpx;
  border-radius: 50%;
}
</style>