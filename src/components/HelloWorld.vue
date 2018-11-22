<template>
  <div class="hello">
    <Brick class='0'>
      <Brick class='1'>
        <Brick class='2'/>
        <Brick class='2'/>
      </Brick>
      <Brick class='1'>
        <Brick class='2'>
          <Brick class='3'>
            <Brick class='4'></Brick>
            <Brick class='4'>
              <Brick class='5'></Brick>
            </Brick>
          </Brick>
          <Brick class='3'>
            <Brick class='4'></Brick>
            <Brick class='4'></Brick>
            <Brick class='4'></Brick>
          </Brick>
        </Brick>
      </Brick>
    </Brick>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Brick from '@/components/Brick.vue'; // @ is an alias to /src

@Component({
  components: {
    Brick,
  },
})
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
html, body {
  overflow: hidden;
}

.hello > .wrapper {
  overflow: auto;
}
</style>
