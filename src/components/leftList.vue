<template>
  <div class="small-img-list-component">
    <!-- 小图列表 -->
    <div class="small-img-list">
      <div
        :class="currentIndex === index ? 'item active' : 'item'"
        v-for="(item,index) in imgList"
        :key="'small_' + index"
        @click="setCurrentIndex(index)"
      >
        <a-image :src="item.src" @load="loadFun(index)" :preview="false">
          <template #placeholder>
            <!-- 加载中... -->
            <!-- <a-image src="../../assets/img/mode.png"></a-image> -->
          </template>
        </a-image>
        <div class="bot">
          <span>{{ index + 1 }}/{{ imgList.length }}</span>
        </div>
      </div>
    </div>
    <!-- 跳转页数 -->
    <div class="footer">
      <!-- 合约页数展示 -->
      <span>当前第{{ currentIndex + 1 }}页/共{{ imgList.length }}页</span>
      <!-- 跳转 -->
      <div>
        跳转至
        <input type="text" />页
      </div>
    </div>
    <!-- 收缩小图列表 -->
    <div :class="unfold ? 'hide' : 'hide none'">
      <img src="../../assets/img/hide.png" class="hide-img" alt srcset @click="setUnfold" />
      <img src="../../assets/img/show.png" class="show-img" alt srcset @click="setUnfold" />
    </div>
  </div>
</template>
<script>
export default {
  props: {
    imgList: {
      default: [
        {
          src: "https://eseal.certca.cn:443/api/previewImage?filePath=/upload/pdfImages/20220110/20220110153038635/9fbb95b6bfb14a5eb183f0e20ca29b98_signed_1.png",
          load: false
        },
        {
          src: "https://eseal.certca.cn:443/api/previewImage?filePath=/upload/pdfImages/20220110/20220110153038635/9fbb95b6bfb14a5eb183f0e20ca29b98_signed_2.png",
          load: false
        },
        {
          src: "https://eseal.certca.cn:443/api/previewImage?filePath=/upload/pdfImages/20220110/20220110153038635/9fbb95b6bfb14a5eb183f0e20ca29b98_signed_3.png",
          load: false
        },
        {
          src: "https://eseal.certca.cn:443/api/previewImage?filePath=/upload/pdfImages/20220110/20220110153038635/9fbb95b6bfb14a5eb183f0e20ca29b98_signed_4.png",
          load: false
        },
        {
          src: "https://eseal.certca.cn:443/api/previewImage?filePath=/upload/pdfImages/20220110/20220110153038635/9fbb95b6bfb14a5eb183f0e20ca29b98_signed_5.png",
          load: false
        }
      ],
      type: Array,
    },
    unfold: {
      default: true,
      type: Boolean
    }
  },
  data() {
    return {
      currentIndex: 0,//当前选项
    }
  },
  methods: {

    setUnfold() {
      this.$emit('setUnfold')
    },
    setCurrentIndex(index) {
      this.currentIndex = index
    },
  }
}
</script>
<style lang="less" scoped>
.small-img-list-component {
  height: fit-content;
  min-height: 100%;
  position: relative;
  padding-bottom: 40px;

  .small-img-list {
    .item {
      display: flex;
      width: 100%;
      flex-direction: column;
      align-items: center;
      cursor: pointer;
      :deep(.ant-image) {
        text-align: center;
        padding-top: 15px;
        margin-bottom: 15px;
        min-height: 100px;
        min-width: 100px;
        .ant-image-img {
          width: 90%;
          border: 1px solid @u-border-color;
          border-radius: 0 !important;
          box-sizing: border-box !important;
        }
      }
      &.active {
        :deep(.ant-image) {
          .ant-image-img {
            border: 1px solid @u-type-primary;
          }
        }
        span {
          color: @u-type-primary;
        }
      }
    }
  }
  .footer {
    width: 100%;
    display: flex;
    font-size: 12px;
    height: 40px;
    align-items: center;
    justify-content: space-between;
    padding: 0 10px;
    position: fixed;
    background: #fff;
    bottom: 0;
    left: 0;
    max-width: 200px;
    input {
      border: none;
      border-bottom: 1px solid @u-border-color;
      width: 20px;
      text-align: center;
    }
  }
}
.hide {
  position: fixed;
  left: 185px;
  top: 50%;
  transform: translateY(-50%);
  z-index: 3;
  background: gray;
  cursor: pointer;
  display: block;
  border-radius: 4px 0 0 4px;

  .show-img {
    display: none;
  }
  &.none {
    left: 15px;
    border-radius: 0 4px 4px 0;
    .hide-img {
      display: none;
    }
    .show-img {
      display: block;
    }
  }
  img {
    width: 20px;
    height: 30px;
  }
}
</style>