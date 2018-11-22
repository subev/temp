<template>
  <div class='wrapper'>
     <div class="head">
       <div class='phone'/>
     </div>
     <div class="body">
       <slot name='default'>CHILDREN</slot>
     </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component({
})
export default class Brick extends Vue {

}
</script>
<style scoped lang="scss">

.phone {
  background: red;
  width: 300px;
  height: 100px;
}

.wrapper {
  border: 1px solid yellow;
  display: flex;
  flex: 0 1 100%;
  flex-direction: column;
}

.head {
  display: flex;
  flex-grow: 0;
  flex-shrink: 0;
  padding: 20px;
  border: 1px solid green;
  justify-content: center;

  min-width: 300px;
}

.body {
  border: 1px solid red;
  display: flex;
  justify-content: space-around;
}
</style>
