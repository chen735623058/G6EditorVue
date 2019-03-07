<!-- 流程图 工具栏组件 -->
<template>
    <div id="toolbar" class="toolbar">
        <i data-command="undo" class=" command iconfont icon-chexiao"  title="撤销"></i>
        <i data-command="redo" class=" command iconfont icon-zhongzuo" title="重做"></i>
        <span className="separator"></span>
        <i data-command="copy" class=" command iconfont icon-fuzhi" title="复制"></i>
        <i data-command="paste" class=" command iconfont icon-niantie" title="粘贴"></i>
        <i data-command="delete" class=" command iconfont icon-shanchu" title="删除"></i>
        <span className="separator"></span>
        <i data-command="zoomIn" class=" command iconfont icon-fangda" title="放大"></i>
        <i data-command="zoomOut" class=" command iconfont icon-suoxiao" title="缩小"></i>
        <i data-command="autoZoom" class=" command iconfont icon-full-screen" title="适应画布"></i>
        <i data-command="resetZoom" class=" command iconfont icon-normal" title="实际尺寸"></i>
        <span className="separator"></span>
        <i data-command="toBack" class=" command iconfont icon--qianzhi" title="层级后置"></i>
        <i data-command="toFront" class=" command iconfont icon--houzhi" title="层级前置"></i>
        <span className="separator"></span>
        <i data-command="multiSelect" class=" command iconfont icon-RectangleCopy" title="多选"></i>
        <i data-command="addGroup" class=" command iconfont icon-zuhe" title="成组"></i>
        <i data-command="unGroup" class=" command iconfont icon-jiezhiya" title="解组"></i>
    </div>
</template>
<script>
    import G6Editor from '@antv/g6-editor';
    export default {
        data(){
            return{

            }
        },
        props: ['editor'],
        mounted() {
            const toolbar = new G6Editor.Toolbar({
                container: 'toolbar',
            });
            this.editor.add(toolbar)
        }
    }
</script>
<style>
    @import "../assets/iconfont.css";
    .toolbar{
        padding: 8px 0px;
        width: 100%;
        border: 1px solid #E9E9E9;
        height: 42px;
        z-index: 3;
        box-shadow: 0px 8px 12px 0px rgba(0, 52, 107, 0.04);
        position: absolute;
    }
    .toolbar *::before{
        font-size: 16px !important;
    }
    .toolbar .disable{
        color: rgba(0,0,0,0.25);
    }
    .toolbar .icon-select.disable{
        background: #EEEEEE;
    }
    .toolbar .separator{
        margin: 4px;
        border-left: 1px solid #E9E9E9;
    }
    .toolbar .command{
        width: 27px;
        height: 27px;
        margin: 0px 6px;
        border-radius: 2px;
        padding-left: 4px;
        display: inline-block;
        border: 1px solid rgba(2,2,2,0);
    }
    .toolbar .command:nth-of-type(1){
        margin-left: 24px;
    }
    .toolbar .command:hover{
        cursor: pointer;
        color: darkgoldenrod;
    }
    .toolbar .disable:hover{
        cursor: default;
        color: aquamarine;
    }
</style>