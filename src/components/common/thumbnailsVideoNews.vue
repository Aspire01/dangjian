<template>
  <div>
    <!-- 这里是缩略图新闻组件 -->
    <div class="mx-thumbnails-wrapper">
      <div class="mx-thumbnails mx-thumbnails-cos2">
        <ul class="clearfix course">
          <!-- 一个li start -->
          <li v-for="item in (latestList || '').slice(0,4)" :key="item.id">
            <div class="mx-thumbnails-box">
              <a href="javascript:;" @click="goDetails(item)">
                <img :src="item.imageUrl?item.imageUrl:''" alt />
                <span>
                  <!-- 播放图标需要定位 -->
                  <template v-if="item.type==0"></template>
                  <template v-if="item.type==1">
                    <i class="iconfont icon-yinpin"></i>
                  </template>
                  <template v-if="item.type==2">
                    <i class="iconfont icon-caret-right"></i>
                  </template>
                  {{item.title}}
                </span>
              </a>
            </div>
          </li>
          <!-- 一个li end -->
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    latestList: {}
  },
  data() {
    return {
      ipAddress: ""
    };
  },
  created() {
    //赋值数据
    this.ipAddress = this.$store.state.ipAddress;
  },
  methods: {
    //传递item, 获取item项中必要的参数
    goDetails(item) {
      // console.log(item.id);
      // 判断type类型
      if (item.type == 0) {
        //普通文章页
        this.$router.push({
          path: "/details-news",
          query: { categoryId: item.categoryId, id: item.id, type: item.type }
        });
        // this.saveDetailParams();
      }
      if (item.type == 1) {
        // 音频详情页
        this.$router.push({
          path: "/details-radio",
          query: { categoryId: item.categoryId, id: item.id, type: item.type }
        });
        // this.saveDetailParams();
      }
      if (item.type == 2) {
        //视频详情页
        this.$router.push({
          path: "/details-video",
          query: { categoryId: item.categoryId, id: item.id, type: item.type }
        });
        // this.saveDetailParams();
      }
    }
  }
};
</script>

<style scoped="scoped" lang="scss">
/*移动端 低于960 111*/
@media only screen and (max-width: 959px) {
  $times: 2;
  .mx-thumbnails-wrapper {
    /*移动端默认100宽度*/
    width: 100vw;
  }
  /*2 倍距离*/
  .mx-thumbnails ul {
    margin: 0;
  }
  .mx-thumbnails ul li {
    width: 50%;
    margin-top: 0;
    padding: 15px * $times 15px * $times 5px * $times;
    background-color: #fff;
  }
  .mx-thumbnails ul span {
    display: block;
    line-height: 22px * $times;
    height: 54px * $times;
    font-size: 12px * $times;
    overflow: hidden;
    padding: 10px * $times 0 0;
    border-bottom-width: 10px * $times;
  }
  .mx-thumbnails-cos2 ul li {
    width: 50%;
  }

  .mx-thumbnails-cos2 ul span {
    font-size: 12px * $times;
    line-height: 18px * $times;
  }
  .mx-thumbnails-box {
    display: block;
    background-color: #fff;
    padding: 56% 0 4px * $times;
    /* 给图片做定位点 */
    position: relative;
  }

  /* 字体图标边框设置 ，用于音频 视频按钮 */
  .mx-thumbnails-box i {
    position: absolute;
    left: 10px * $times;
    top: -38px * $times;
    width: 32px * $times;
    height: 32px * $times;
    line-height: 28px * $times;
    border-radius: 100px;
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    border: 2px rgba(255, 255, 255, 0.8) solid;
    text-align: center;
    font-size: 18px * $times;
    margin-top: 56%;
  }

  .mx-thumbnails-sum {
    margin: 5px * $times 0 0;
    padding: 0;
    line-height: 20px * $times;
    height: 40px * $times;
    font-size: 12px * $times;
    color: #aaa;
    overflow: hidden;

    background-color: #fff;
  }

  .mx-thumbnails-info {
    margin-top: 5px * $times;
    padding: 0;
    line-height: 20px * $times;
    height: 20px * $times;
    font-size: 12px * $times;

    color: #aaa;
    overflow: hidden;
  }
  .mx-thumbnails-info a {
    font-size: 12px * $times;
  }
  .mx-thumbnails-info em {
    font-size: 12px * $times;
  }
}
/* 960 -1240尺寸 */
@media only screen and (min-width: 960px) and (max-width: 1239px) {
  .mx-thumbnails-box{
    padding: 56% 0 4px;
  }
}
</style>
