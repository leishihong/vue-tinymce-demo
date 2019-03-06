<template>
  <div>
    <!--<MainEditor
          :config           = "Config"
          v-model          = "Value"
          :url              = "Url" //图片上传地址
          :max-size         = "MaxSize"//文件上传最大值
          :accept           = "Accept"//接收什么格式的图片
          :with-credentials = false
          @on-ready         = "onEditorReady"//后面什么的没研究了
          @on-destroy       = "onEditorDestroy"
          @on-upload-success= "onEditorUploadComplete"
          @on-upload-fail   = "onEditorUploadFail"
        ></MainEditor>-->
    <!-- 富文本 -->
    <h1>tinymce</h1>
    <MainEditor v-model="Value" @on-upload-complete="onEditorUploadComplete"></MainEditor>
    <h1>vue-ueditor-wrap兼容性不好IE10以上</h1>
    <!-- 你不需要担心一个页面中过多vue-ueditor-wrap组件会导致混乱,或者重复引用JS(打开控制台瞄一眼),每个组件都保证拥有一个独立的UEditor实例,你可以尝试把数字改成99(根据自己电脑自行斟酌),但依然稳定可用 -->
    <vue-ueditor-wrap v-model="Value" :destroy="false" :config="config"></vue-ueditor-wrap>
  </div>
</template>

<script >
window.tinymce.baseURL = '/static/tinymce'
window.tinymce.suffix = '.min'
import MainEditor from './editor.vue'
import VueUeditorWrap from 'vue-ueditor-wrap'
export default {
  props: [],
  name: '',
  data() {
    return {
      Value: '<p>ejjrgjkg</p></br><h1>标题显示</p>',
      config: {
        toolbars: [
          [
            'undo', //撤销
            'redo', //重做
            'bold', //加粗
            'indent', //首行缩进
            'italic', //斜体
            'underline', //下划线
            'strikethrough', //删除线
            'subscript', //下标
            'fontborder', //字符边框
            'superscript', //上标
            'formatmatch', //格式刷
            'justifyleft', //居左对齐
            'justifyright', //居右对齐
            'justifycenter', //居中对齐
            'justifyjustify', //两端对齐
            'forecolor', //字体颜色
            'backcolor', //背景色
            'insertorderedlist', //有序列表
            'insertunorderedlist', //无序列表
            'preview', //预览
            'horizontal', //分隔线
            'insertrow', //前插入行
            'insertcol', //前插入列
            'inserttitle', //插入标题
            'cleardoc', //清空文档
            'fontfamily', //字体
            'fontsize', //字号
            'paragraph', //段落格式
            'insertimage', //多图上传
            'link', //超链接
            'emotion', //表情
            'spechars', //特殊字符
            'fullscreen', //全屏
            'directionalityltr', //从左向右输入
            'directionalityrtl', //从右向左输入
            'rowspacingtop', //段前距
            'rowspacingbottom', //段后距
            'imagenone', //默认
            'attachment', //附件
            'imagecenter', //居中
            'wordimage', //图片转存
            'lineheight', //行间距
            'edittip ', //编辑提示
            'customstyle', //自定义标题
            'autotypeset', //自动排版
            'touppercase', //字母大写
            'tolowercase', //字母小写
          ]
        ],
        // 编辑器不自动被内容撑高
        autoHeightEnabled: false,
        // 初始容器高度
        initialFrameHeight: 400,
        // 初始容器宽度
        initialFrameWidth: '100%',
        // 上传文件接口（这个地址是我为了方便各位体验文件上传功能搭建的临时接口，请勿在生产环境使用！！！）
        // http://ueditor.lys.muxiongit.com/UEditor/php/controller.php?action=uploadimage
        serverUrl: '', // 注意需要后台设置图片地址  有缺陷  每次打包以往资源会丢失
        // UEditor 资源文件的存放路径，如果你使用的是 vue-cli 生成的项目，通常不需要设置该选项，vue-ueditor-wrap 会自动处理常见的情况，如果需要特殊配置，参考下方的常见问题2
        // UEDITOR_HOME_URL: '/static/UEditor/'
        // 配合最新编译的资源文件，你可以实现添加自定义Request Headers,详情https://github.com/HaoChuan9421/ueditor/commits/dev-1.4.3.3
        // headers: {
        //   access_token: '37e7c9e3fda54cca94b8c88a4b5ddbf3'
        // }
      }
    }
  },
  components: {
    MainEditor,
    VueUeditorWrap,
  },
  computed: {

  },
  mounted() {
    // 如果没有定时器 || 定时器时间低于500ms(视电脑硬件配置及代码量)，会出现报错
    setTimeout(() => {
      window.tinymce.activeEditor.setContent(this.Value)
    }, 1000);
  },
  methods: {
    // 回调方法处理
    onEditorUploadComplete(res) {
      console.log(res);
    },
  }
}
</script>

