<template>
  <div id="app">
    <div style="height: 500px; width: 500px; margin: 20px; border: 1px solid red; position: relative;">
      <VueDraggableResizable
        class="demo"
        v-bind="box"
        :parent="true"
        :deselect-exclude="['.deselect-exclude']">
        <p>Custom handles slot</p>
        <template slot="handles" slot-scope="{ handlesConf }">
          <div
            v-for="handle in handlesConf.handles"
            v-if="handlesConf.resizable"
            class="custom-handle"
            :key="handle"
            :class="'custom-handle-' + handle"
            :style="{ display: handlesConf.enabled ? 'block' : 'none'}"
            @mousedown="handlesConf.handleDown(handle, $event)"
            @touchstart="handlesConf.handleDown(handle, $event)"
          ></div>
        </template>
      </VueDraggableResizable>
    </div>
    <div class="deselect-exclude" style="height: 500px; width: 500px; margin: 20px; border: 1px solid red; position: relative;">
      <p>deselect exclude btn</p>
      <div>x <input type="number" v-model.number="box.x"></div>
      <div>y <input type="number" v-model.number="box.y"></div>
      <div>w <input type="number" v-model.number="box.w"></div>
      <div>h <input type="number" v-model.number="box.h"></div>
    </div>
    <div style="height: 500px; width: 500px; margin: 20px; border: 1px solid red; position: relative;">
      <VueDraggableResizable :x="50" :y="50" :w="400" :h="400" :parent="true">
        <p>Component</p>
      </VueDraggableResizable>
    </div>
    <div style="height: 500px; width: 500px; margin: 20px; border: 1px solid red; position: relative;">
      <h2>Grid 30x30</h2>
      <VueDraggableResizable :x="50" :y="50" :w="400" :h="400" :grid="[30, 30]" :parent="true">
      <p>Component</p>
      </VueDraggableResizable>
    </div>
    <div style="height: 500px; width: 500px; margin: 20px; border: 1px solid red; position: relative;">
      <h2>Custom handler</h2>
      <VueDraggableResizable :x="50" :y="50" :w="150" :h="50" :parent="true" :resizable="false" :dragHandle="'.dragHandle'">
        <p>Component</p>
        <span class="dragHandle">
          =
        </span>
      </VueDraggableResizable>
    </div>
    <div style="height: 500px; width: 500px; margin: 20px; border: 1px solid red; position: relative;">
      <h2>Grid 30x30 and handler</h2>
      <VueDraggableResizable :x="50" :y="50" :w="150" :h="50" :parent="true" :grid="[30, 30]" :resizable="false" :dragHandle="'.dragHandle'">
        <p>Component</p>
        <span class="dragHandle">
          =
        </span>
      </VueDraggableResizable>
    </div>
  </div>
</template>

<script>
import VueDraggableResizable from './components/vue-draggable-resizable'

export default {
  name: 'app',
  components: {
    VueDraggableResizable
  },
  data () {
    return {
      box: {
        x: 10,
        y: 10,
        w: 100,
        h: 100
      }
    }
  }
}
</script>

<style>
  .demo {
    background: rgba(0,92,249,.4);
    border: 2px solid rgba(0,92,249,1);
  }
  h2 {
    opacity: 0.3;
    padding: 0 0 0 20px;
    z-index: -1;
  }
  .dragHandle {
    position: absolute;
    top: 0;
    right: 0;
    padding: 6px;
    font-size: 20px;
  }
  .vdr {
    /* background: white; */
  }
  .custom-handle {
    box-sizing: border-box;
    display: none;
    position: absolute;
    width: 12px;
    height: 12px;
    font-size: 1px;
    background: #fff;
    border: 2px solid #005CF9;
    border-radius: 50%;
  }
  .custom-handle-tl {
    top: -6px;
    left: -6px;
    cursor: nw-resize;
  }
  .custom-handle-tm {
    top: -6px;
    left: 50%;
    margin-left: -6px;
    cursor: n-resize;
  }
  .custom-handle-tr {
    top: -6px;
    right: -6px;
    cursor: ne-resize;
  }
  .custom-handle-ml {
    top: 50%;
    margin-top: -6px;
    left: -6px;
    cursor: w-resize;
  }
  .custom-handle-mr {
    top: 50%;
    margin-top: -6px;
    right: -6px;
    cursor: e-resize;
  }
  .custom-handle-bl {
    bottom: -6px;
    left: -6px;
    cursor: sw-resize;
  }
  .custom-handle-bm {
    bottom: -6px;
    left: 50%;
    margin-left: -6px;
    cursor: s-resize;
  }
  .custom-handle-br {
    bottom: -6px;
    right: -6px;
    cursor: se-resize;
  }
</style>
