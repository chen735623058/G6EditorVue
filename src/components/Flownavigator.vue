<!-- 流程图 导航缩略图组件 -->
<template>
    <div id="navigator">
        <div class="pannel-title">导航器</div>
        <div id="minimap"></div>
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
            const minimap = new G6Editor.Minimap({
                container: 'minimap',
            });
            this.editor.add(minimap);
        }
    }
</script>
<style>
    #navigator {
        width: 200px;
        height: 176px;
        position: absolute;
        bottom: 0px;
        right: 0px;
        z-index: 3;
    }

    #navigator .slider{
        margin: 7px 10px 10px;
        float: left;
        width: 120px;
    }
    #navigator #minimap{
        width: 200px;
        height: 120px;
    }
</style>