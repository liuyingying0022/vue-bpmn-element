<template>
  <div>
    <el-button-group>
<!--      <el-button type="primary" size="mini" title="保存并发布" icon="el-icon-s-order">保存并发布</el-button>-->
<!--      <el-button type="primary" size="mini" title="保存草稿" icon="el-icon-s-order">保存草稿</el-button>-->
<!--      <el-button type="primary" size="mini" title="打开流程文件" icon="el-icon-s-open"></el-button>-->
<!--      <el-button type="primary" size="mini" title="创建新流程图" icon="el-icon-circle-plus"></el-button>-->
      <el-button type="primary" size="mini" title="下载流程图" icon="el-icon-picture" @click="downBpmnSvg">下载流程图</el-button>
      <el-button type="success" size="mini" title="下载流程文件" icon="el-icon-download" @click="downXmlFile">下载流程文件XML</el-button>
      <el-button type="warning" size="mini" title="下载流程文件" icon="el-icon-download" @click="downBpmnFile">下载流程文件BPMN</el-button>
<!--      <el-button title="撤销" size="mini" icon="el-icon-refresh-left"></el-button>-->
<!--      <el-button title="恢复" size="mini" icon="el-icon-refresh-right"></el-button>-->
<!--      <el-button title="恢复" size="mini" icon="el-icon-zoom-in"></el-button>-->
<!--      <el-button title="恢复" size="mini" icon="el-icon-zoom-out"></el-button>-->
<!--      <el-button title="重置" size="mini" icon="el-icon-rank"></el-button>-->
      <el-button title="预览" size="mini" icon="el-icon-s-opportunity" @click="xmlVisible = !xmlVisible">预览</el-button>
    </el-button-group>

    <el-dialog :visible.sync="xmlVisible" title="流程" :fullscreen="false" top="10vh">
      <vue-ace-editor v-model="processData.xml"
                      lang="xml"
                      @init="editorInit"
                      theme="chrome"
                      width="100%"
                      height="400"
                      :options="{wrap: true, readOnly: true}">
      </vue-ace-editor>
    </el-dialog>
  </div>
</template>

<script>
  import VueAceEditor from 'vue2-ace-editor'
  import './vue-bmpn.css'
  export default {
    name: "ViewerHeader",
    data(){
      return {
        xmlVisible:false
      }
    },
    props:{
      processData:{
        type:Object
      }
    },
    components:{
      VueAceEditor
    },
    methods:{
      editorInit: function () {
        require('brace/ext/language_tools') //language extension prerequsite...
        require('brace/mode/xml')    //language
        require('brace/theme/chrome')
      },
      downXmlFile(){
        this.$emit("handleExportXmlAction");
      },
      downBpmnFile(){
        this.$emit("handleExportBpmnAction");
      },
      downBpmnSvg(){
        this.$emit("handleExportSvgAction")
      }
    }
  }
</script>

<style scoped>
  .icon-header{
    font-size: 14px;
  }

</style>
