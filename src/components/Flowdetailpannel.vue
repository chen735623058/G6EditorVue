<!-- 流程图 属性配置组件 -->
<template>
    <div class="detailpannel" id="detailpannel">
        <div data-status="node-selected" class="pannel">
            <div class="pannel-title">节点属性栏</div>
            <div class="block-container">
                节点属性栏
            </div>
        </div>
        <div data-status="edge-selected" class="pannel" > <!-- 这个地方一定要用class名字为pannel -->
            <div class="pannel-title">边</div>
            <div class="block-container">
                边
            </div>
        </div>
        <div data-status="group-selected" class="pannel" >
            <div class="pannel-title">组</div>
            <div class="block-container">
                组
            </div>
        </div>
        <div data-status="canvas-selected" class="pannel" >
            <div class="pannel-title">画布</div>
            <div class="block-container">
                画布
            </div>
        </div>
        <div data-status="multi-selected" class="pannel" >
            <div class="pannel-title">多选</div>
            <div class="block-container">
                多选
            </div>
        </div>
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
            const detailpannel = new G6Editor.Detailpannel({
                container: 'detailpannel',
            });
            this.editor.add(detailpannel)
        }
    }
</script>
<style>
    .detailpannel{
        height: 100%;
        position: absolute;
        right: 0px;
        z-index: 2;
        background: #F7F9FB;
        width: 200px;
        border-left: 1px solid #E6E9ED;
    }
    .detailpannel .pannel{
        display: none
    }

    .detailpannel .block-container{
        padding: 16px 8px;
    }
    .pannel-title{
        height: 32px;
        border-top: 1px solid #DCE3E8;
        border-bottom: 1px solid #DCE3E8;
        background: #EBEEF2;
        color: #000;
        line-height: 28px;
        padding-left: 12px;
    }
</style>