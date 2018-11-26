<template>
  <div class='wrapper' :id='id'>
     <div class="head">
       <div class='phone'/>
     </div>
     <div class="body">
       <slot name='default'></slot>
     </div>
     <template v-if='id'>
       <div id='draw-layer'>
       </div>
     </template>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from 'vue-property-decorator';

@Component({
})
export default class Brick extends Vue {
  @Prop()
  id: string;
}
</script>
<style lang="scss">

* {
  transition: all .3s;
}

.phone {
  background: red;
  width: 300px;
  height: 100px;
}

.hello > .wrapper {
  min-width: 100%;
}

#mainBrick {
  position: relative;

  #draw-layer {
    position: absolute;
    height: 100%;
    width: 100%;
  }
}

.hello {
  overflow: scroll;
  height: 100%;
}

.wrapper {
  padding: 5px;
  // border-width: 3px  3px 0px  3px;
  // border-style:solid solid solid solid;
  // border-color: #00000010;
  display: inline-flex;
  flex: 0 1 100%;
  flex-direction: column;
}

.head {
  margin-top: 100px;
  display: inline-flex;
  min-width: 100%;
  flex-grow: 0;
  flex-shrink: 0;
  justify-content: center;

  min-width: 300px;
}

.body {
  display: inline-flex;
  min-width: 100%;
  justify-content: space-around;
}
</style>
