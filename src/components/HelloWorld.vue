<template>
  <div class="viewport">
    <div class="hello" tabindex="-1" @keydown.up="inc" @keydown.down="dec">
      <Brick class='0' :style="this.style">
        <Brick class='1'>
        </Brick>
        <Brick class='1'>
          <Brick/>
          <Brick/>
          <Brick>
            <Brick>
              <Brick>
                <Brick>
                <Brick>
                  <Brick/>
                </Brick>
                </Brick>
              </Brick>
            </Brick>
          </Brick>
          <Brick/>
        </Brick>
      </Brick>
    </div>
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

  scale: number = .2;

  inc() {
    this.scale += 0.1;
  }

  dec() {
    this.scale -= 0.1;
  }


  get style() {
    return {
      transform: `scale(${this.scale})`
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
html, body {
}

.hello {

}


.viewport {
  border: 3px solid black;
  height: 1000px;
  width: 1000px;
  margin: auto;
}

.hello > .wrapper {
  //overflow: auto;
}
</style>
