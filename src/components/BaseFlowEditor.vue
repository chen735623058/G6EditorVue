<!-- 流程图入口main组件（主要是设置一些基础属性 初始化editor对象） -->
<template>
    <div style="height: 100%">
        <div class="editor">
              <!-- 缩略图 DOM 结构规约参考 Minimap API -->
            <flowtoolbar :editor="editor" ></flowtoolbar>     <!-- 工具栏 DOM 结构规约参考 Toolbar API -->
            <div style="height: 42px;"></div>
            <div class="bottom-container">
                <flowitempannel :editor="editor"></flowitempannel>
                <flowdetailpannel :editor="editor"></flowdetailpannel>
                <flownavigator :editor="editor"></flownavigator>
                <flowpage :editor="editor"></flowpage>   <!-- 参考 Flow、Mind API -->
            </div>

        </div>

    </div>
</template>

<script>
    import G6Editor from '@antv/g6-editor';
    import flowtoolbar  from './FlowToolbar'
    import flowitempannel  from './FlowItempannel'
    import flowdetailpannel  from './Flowdetailpannel'
    import flownavigator  from './Flownavigator'
    import flowpage  from './Flowpage'
    export default {
        components:{
            flowtoolbar,
            flowitempannel,
            flowdetailpannel,
            flownavigator,
            flowpage
        },
        data(){
            return{
                myFlow:null,
                editor:null,
                selectedModel: {}, // 当前选中项数据模型
                curZoom: 1, // 当前缩放比率
                minZoom: 0.5, // 最小缩放比率
                maxZoom: 2 // 最大缩放比率
            }
        },
        methods:{
            changeZoom(zoom) {
                const editor = this.editor;
                const page = editor.getCurrentPage();
                page.zoom(zoom);
            },
            toggleGrid(ev) {
                const editor = this.editor;
                const page = editor.getCurrentPage();
                if (ev.target.checked) {
                    page.showGrid();
                } else {
                    page.hideGrid();
                }
            },
            updateGraph(key, value) {
                const editor = this.editor;
                editor.executeCommand(() => {
                    const page = editor.getCurrentPage();
                    const selectedItems = page.getSelected();
                    selectedItems.forEach(item => {
                        const updateModel = {};
                        updateModel[key] = value;
                        page.update(item, updateModel);
                    });
                });
            },
            registerGAmenode(){
                // 注册节点基类
                this.myFlow.registerNode('model-card', {
                    draw(item) {
                        const group = item.getGraphicGroup();
                        const model = item.getModel();
                        const width = 184;
                        const height = 40;
                        const x = -width / 2;
                        const y = -height / 2;
                        const borderRadius = 4;
                        const keyShape = group.addShape('rect', {
                            attrs: {
                                x,
                                y,
                                width,
                                height,
                                radius: borderRadius,
                                fill: 'white',
                                stroke: '#CED4D9'
                            }
                        });
                        // 左侧色条
                        group.addShape('path', {
                            attrs: {
                                path: [
                                    [ 'M', x, y + borderRadius ],
                                    [ 'L', x, y + height - borderRadius ],
                                    [ 'A', borderRadius, borderRadius, 0, 0, 0, x + borderRadius, y + height ],
                                    [ 'L', x + borderRadius, y ],
                                    [ 'A', borderRadius, borderRadius, 0, 0, 0, x, y + borderRadius ]
                                ],
                                fill: this.color_type
                            }
                        });
                        // 类型 logo
                        group.addShape('image', {
                            attrs: {
                                img: this.type_icon_url,
                                x: x + 16,
                                y: y + 12,
                                width: 20,
                                height: 16
                            }
                        });
                        // 名称文本
                        const label = model.label ? model.label : this.label;
                        group.addShape('text', {
                            attrs: {
                                text: label,
                                x: x + 52,
                                y: y + 13,
                                textAlign: 'start',
                                textBaseline: 'top',
                                fill: 'rgba(0,0,0,0.65)'
                            }
                        });
                        // 状态 logo
                        group.addShape('image', {
                            attrs: {
                                img: this.state_icon_url,
                                x: x + 158,
                                y: y + 12,
                                width: 16,
                                height: 16
                            }
                        });
                        return keyShape;
                    },
                    // 设置锚点
                    anchor: [
                        [ 0.5, 0 ], // 上面边的中点
                        [ 0.5, 1 ] // 下边边的中点
                    ]
                });

                // 开始节点
                this.myFlow.registerNode('planning-start-node', {
                    label: '起始节点（初始参数）',
                    color_type: '#FAAD14',
                    type_icon_url: 'https://gw.alipayobjects.com/zos/rmsportal/czNEJAmyDpclFaSucYWB.svg',
                    state_icon_url: 'https://gw.alipayobjects.com/zos/rmsportal/MXXetJAxlqrbisIuZxDO.svg',
                    // 设置锚点
                    anchor: [
                        [ 0.5, 1, {
                            type: 'output'
                        }]
                    ]
                }, 'model-card');
            }
        },
        created(){
            this.editor = new G6Editor();
            this.myFlow = G6Editor.Flow;
            this.registerGAmenode();
        },
        mounted() {

            // const pages = this.editor.getComponentsByType('page');
            // // const page = editor.getCurrentPage();
            // const _self = this;
            // pages.forEach(page => {
            //     page.on('afteritemselected', ev => {
            //         _self.selectedModel = ev.item.getModel()
            //     });
            //     page.on('afterzoom', ev => {
            //         _self.curZoom = ev.updateMatrix[0]
            //     });
            // });
        },
    }

</script>
<style>
    .editor canvas {
        display: block;
    }
    .editor{
        position: relative;
        width: 100%;
        height: 100%;
        user-select: none;
        -moz-user-select: none;
        -webkit-user-select: none;
        -ms-user-select: none;
    }
    .page{
        margin-left: 200px;
        margin-right: 200px;
        height: 100%;
    }

    .bottom-container {
        position: relative;
        height: calc(100% - 42px);
    }


    .pannel-title {
        height: 32px;
        border-top: 1px solid #DCE3E8;
        border-bottom: 1px solid #DCE3E8;
        background: #EBEEF2;
        color: #000;
        line-height: 28px;
        padding-left: 12px;
    }

</style>