<script setup>

console.log("stepup")
</script>

<style>
/* 引入icon图标 */
@import "@/static/image-iconfont/iconfont.css";

/*每个页面公共css */
 ::v-deep .uni-popup__wrapper{
    width: 80%;
    
}
body {
margin: 0;  /* 如果页面出现垂直滚动条，则加入此行CSS以消除之 */
}
pages{
  height: 100vh;
}
uni-left-window{
  margin-right: 1rem;
  background: white;
  padding-right: 2rem;
}
@media (max-width: 900px) {
  uni-left-window {
    display: none;
  }
}
.uni-forms{
  width: 90%;
  max-width: 410px;
}
.main-header{
  display: none;
}
::v-deep .el-container{
    width: 99%;
    height: 95%;
}
::v-deep .right-toolbar-con{
    width: 100% !important;
    text-align: right !important;
}
::v-deep .right-toolbar{
  max-width: 200px !important;
}
</style>
