<!-- 流程图 主画布组件 -->
<template>
    <div id="page" class="page"></div>
</template>
<script>
    import G6Editor from '@antv/g6-editor';
    export default {
        data(){
            return{

            }
        },
        props:['editor'],
        methods:{
            myinit(){
                const height = window.innerHeight - 42;
                const page = new G6Editor.Flow({
                    graph: {
                        container: 'page',
                        height,
                        fitView:'tl'
                    },
                    align: {
                        item: 'horizontal',
                        grid: 'cc'
                    },
                    grid:{
                        cell: 20,
                        line:{}
                    },
                    noEndEdge : false // 不允许悬空边
                });
                page.changeAddEdgeModel({
                    shape: "flow-polyline-round"
                });
                // 输入锚点不可以连出边
                page.on('hoveranchor:beforeaddedge', ev => {
                    if (ev.anchor.type === 'input') {
                        ev.cancel = true;
                    }
                });
                page.on('dragedge:beforeshowanchor', ev => {
                    // 只允许目标锚点是输入，源锚点是输出，才能连接
                    if (!(ev.targetAnchor.type === 'input' && ev.sourceAnchor.type === 'output')) {
                        ev.cancel = true;
                    }
                    // 如果拖动的是目标方向，则取消显示目标节点中已被连过的锚点
                    if (ev.dragEndPointType === 'target' && page.anchorHasBeenLinked(ev.target, ev.targetAnchor)) {
                        ev.cancel = true;
                    }
                    // 如果拖动的是源方向，则取消显示源节点中已被连过的锚点
                    if (ev.dragEndPointType === 'source' && page.anchorHasBeenLinked(ev.source, ev.sourceAnchor)) {
                        ev.cancel = true;
                    }
                });
                this.editor.add(page);
            }
        },
        mounted(){
            this.myinit();
        }
    }
</script>