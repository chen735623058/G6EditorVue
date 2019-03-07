<!-- 流程图 原件配置组件 -->
<template>
    <div class="itempannel" id="itempannel">
        <img draggable="false" src="https://gw.alipayobjects.com/zos/rmsportal/ZnPxbVjKYADMYxkTQXRi.svg" data-type="node" data-shape="flow-circle" data-size="72*72" data-color="#FA8C16" data-label="起止节点" class="getItem" />
        <img draggable="false" src="https://gw.alipayobjects.com/zos/rmsportal/wHcJakkCXDrUUlNkNzSy.svg" data-type="node" data-shape="flow-rect" data-size="80*48" data-color="#1890FF" data-label="常规节点" class="getItem" />
        <img draggable="false" src="https://gw.alipayobjects.com/zos/rmsportal/SnWIktArriZRWdGCnGfK.svg" data-type="node" data-shape="flow-rhombus" data-size="80*72" data-color="#13C2C2" data-label="分叉节点" class="getItem" />
        <img draggable="false" src="https://gw.alipayobjects.com/zos/rmsportal/rQMUhHHSqwYsPwjXxcfP.svg" data-type="node" data-shape="flow-capsule" data-size="80*48" data-color="#722ED1" data-label="模型节点" class="getItem" />
        <ul>
            <li class="getItem" data-shape="planning-start-node" data-type="node" data-size="170*34">
                <span class="panel-type-icon"></span>开始
            </li>
        </ul>

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
            const itempannel = new G6Editor.Itempannel({
                container: 'itempannel',
            });
            this.editor.add(itempannel)
        }
    }
</script>
<style>
    .itempannel{
        height: 100%;
        position: absolute;
        left: 0px;
        z-index: 2;
        background: #F7F9FB;
        width: 200px;
        padding-top: 8px;
        border-right: 1px solid #E6E9ED;
    }
    .itempannel img{
        width: 92px;
        height: 96px;
        padding: 4px;
        margin-left: 4px;
        border-radius: 2px;
        border: 1px solid rgba(0,0,0,0);
    }
    .itempannel img:hover{
        cursor: move;
        border: 1px solid #ccc;
    }
    .itempannel ul{
        padding: 0px;
        padding-left: 16px;
    }
    .itempannel li{
        color: rgba(0,0,0,0.65);
        border-radius: 4px;
        width: 160px;
        height: 28px;
        line-height: 26px;
        padding-left: 8px;
        border: 1px solid rgba(0,0,0,0);
        list-style-type: none;
    }

    .itempannel .panel-type-icon{
        width: 16px;
        height: 16px;
        display: inline-block;
        vertical-align: middle;
        margin-right: 8px;
        background: url(https://gw.alipayobjects.com/zos/rmsportal/czNEJAmyDpclFaSucYWB.svg)
    }
    .itempannel li:hover{
        background: white;
        border: 1px solid #CED4D9;
        cursor: move;
    }
</style>