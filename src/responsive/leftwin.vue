<template>
  <scroll-view style="height: 100%;" scroll-y="true">
    <view class="flex-c-between-start h-full">
      <view class="w-full">
        <view class="flex-start-center m-30 pad_Left">
          <img src="@/assets/logo/logo.png" width="32px" height="34px"/>
          <span class="m-l-10" style="font-weight: bold; font-size: 24px;">常州中电</span>
        </view>

        <view class="flex-start-center m-y-30 m-l-22">
          <image src="../static/shu.png" mode="scaleToFill" style="width:2%;height:1.7rem;margin-right:1rem"/>
          <h3 class="m-l-5">{{ left_title }}</h3>
        </view>
      </view>

      <view class="h-full w-full text-left m-l-10 noMargin">
        <template v-for="(item, index) in dynamicRoutes" :key="item.path">
          <navigator
              v-if="item.meta.allShow  || (!item.meta.shownot &&
                (
                    (item.meta.adminShow && (userInfo.admin || userInfo.adminReadOnly))
                    ||
                    (item.meta.changeShow && userInfo.changePerson)
                )
              )"
              :url="item.path"
              open-type="navigate"
              @click="() => { setActiveIndex(index); }"
              :class="activeIndex === index ? 'active-navigator' : ''"
          >
          <uni-icons custom-prefix="iconfont" :type="item.meta.icon" size="25" color="gray" class="icon" />
            <text class="active_text">{{ item.meta.title }}</text>
          </navigator>
        </template>
      </view>

      <!-- <view class="w-full m-b-30">
        <view class="flex-end-center m-r-20">
         
         <image src="@/assets/logo/logo.png" style="width: 30px; height: 30px;" mode="aspectFill"></image> 
        <uni-badge :is-dot="true" :text="1" absolute="rightTop" class="item m-l-20">
            <uni-icons type="chatbubble" size="30"></uni-icons>
          </uni-badge> 
        </view>
      </view> -->
    </view>
  </scroll-view>
</template>

<script setup>
import {dynamicRoutes} from '@/router/dynamic';

const {proxy} = getCurrentInstance();
const left_title = import.meta.env.VITE_APP_NAME;

const activeIndex = ref(null); // 默认高亮第一项

const userInfo = ref({});

const setActiveIndex = (index) => {
  activeIndex.value = index; // 设置当前高亮项
};

onMounted(() => {
  uni.$on('updateRoute', (route) => {
    dynamicRoutes.forEach((page, index) => {
      if (page.path.includes(route)) {
        setActiveIndex(index)
      }
    });

    let strUserInfo = uni.getStorageSync("userInfo") || null;
    if (strUserInfo != null) {
      userInfo.value = JSON.parse(strUserInfo);
    }

  });
});


</script>

<style scoped>
uni-navigator {
  line-height: 3rem;
  border-radius: 1rem;
  box-sizing: border-box;
  height: 3rem;
  transition: background 0.3s, color 0.3s; /* 添加过渡效果 */
}

.navigator-hover {
  opacity: 1 !important;
}

.active_text {
  margin-left: 10px;
  padding-left: 3rem;
}

.active-navigator {
  background: rgb(101, 105, 247);
  color: white;
}

.active-navigator .active_text  {
  color: white !important; /* 确保选中状态下字体颜色为白色 */
}

.noMargin {
  margin: 0 !important;
  padding-left: 10px !important;
  box-sizing: border-box;
}
.icon{
  position: absolute;
  left: 14%;
  size: 28%;
}
.active-navigator .icon {
  color: white !important; /* 确保激活状态下图标颜色为白色 */
}
</style>
