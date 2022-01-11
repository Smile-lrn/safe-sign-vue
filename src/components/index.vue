<template>
  <a-layout class="main-page">
    <!-- <slider :collapsed="collapsed" :selectedKeys="selectedKeys"></slider> -->
    <a-layout>
       <a-layout-header class="header-box" >
         <div class="logo" >
         <img src="../assets/img/logo.png" alt="">
          <span>安全签</span>
         </div>
        <div class="avater-box">
            <a-image
                :width="50"
                :src="`https://zos.alipayobjects.com/rmsportal/jkjgkEfvpUPVyRjUImniVslZfWPnJuuZ.png?${random}`"
                >
                <template #placeholder>
                    <a-image
                    src="https://zos.alipayobjects.com/rmsportal/jkjgkEfvpUPVyRjUImniVslZfWPnJuuZ.png?x-oss-process=image/blur,r_50,s_50/quality,q_1/resize,m_mfit,h_200,w_200"
                    :width="50"
                    :preview="false"
                    />
                </template>
            </a-image>
            <span>lrn</span>
        </div>
      </a-layout-header>
      <a-layout-content >
        <router-view/>
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>
<script>
// import slider from './slider.vue';
import header from './header.vue';
import {  MenuUnfoldOutlined, MenuFoldOutlined,AntDesignOutlined  } from '@ant-design/icons-vue';
import { defineComponent, ref } from 'vue';
export default defineComponent({
  components: {
    MenuUnfoldOutlined,
    MenuFoldOutlined,
    // slider,
    header
  },

  setup() {
    return {
      selectedKeys: ref(['1']),
      collapsed: ref(false),
    };
  },

});
</script>
<style scoped lang="less">
.main-page{
    width: 100%;
    min-width: 900px;
    overflow-x: auto;
    height: 100vh;
    overflow-y: hidden;
}
.trigger {
  font-size: 18px;
  line-height: 64px;
  padding: 0 24px;
  cursor: pointer;
  transition: color 0.3s;
}

.trigger:hover {
  color: #1890ff;
}



.site-layout .site-layout-background {
  background: #fff;
}
.header-box{
    display: flex;
    justify-content: space-between;
    background: @u-type-primary;
    .avater-box{
        display: flex;
        padding: 0 24px;
       .ant-image {
           border: #1890ff;
       }
    }
    .logo{
      display: flex;
      align-items: center;
      img{
        width: 40px;
        height: 40px;
        display: block;
        margin-right: 10px;
      }
      span{
        font-size: 24px;
        color: #fff;
        letter-spacing: 2px;
      }
    }
}
:deep(.ant-image) .ant-image-img{
    border-radius: 50% !important;
}
</style>