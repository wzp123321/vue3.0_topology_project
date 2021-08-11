<template>
  <!-- https://juejin.cn/post/6844904002392424456 -->
  <div class="home">
    <div class="left">left</div>
    <div class="mid">
      <div id="topology_canvas" @contextmenu="onContextMenu($event)"></div>
    </div>
    <div class="right">
      <button @click="onGetData">拿到数据</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted } from 'vue';
import { Topology } from '@topology/core';
import dataJSON from '../mock/data.json';

export default defineComponent({
  setup() {
    let topology: Topology;
    const onContextMenu = (e: any) => {
      console.log(e);
    };
    const onGetData = () => {
      console.log(topology.data);
    };
    onMounted(() => {
      topology = new Topology('topology_canvas', {});
      if (!topology) {
        return;
      }
      topology.open(dataJSON.data);
      topology.render();
      console.log(topology.data);
    });

    return { onContextMenu, onGetData };
  },
});
</script>
<style lang="less" scoped>
.home {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  .left,
  .right {
    width: 200px;
    height: 100%;
  }
  .mid {
    flex: 1;
    * {
      height: 100%;
    }
  }
}
</style>
