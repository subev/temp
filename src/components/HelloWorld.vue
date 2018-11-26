<template>
  <div class="viewport">
    <div class="hello" tabindex="-1" @keydown.up="inc" @keydown.down="dec">
      <div class='scaler' :style="this.style">
        <Brick class='0' id="mainBrick">
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
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import Brick from "@/components/Brick.vue"; // @ is an alias to /src

@Component({
  components: {
    Brick
  }
})
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;

  scale: number = 1;

  inc() {
    this.scale += 0.1;
  }

  dec() {
    this.scale -= 0.1;
  }

  mounted(): void {
    this.initializeDiagram();
  }
  updated(): void {

  }

  initializeDiagram(): void {
    var $ = go.GraphObject.make;
    var diagram = $(
      go.Diagram,
      "draw-layer",
      {
        "isEnabled": false, //this disables all the below and even more
        "animationManager.isEnabled": false,
        "initialPosition": go.Point.parse("0 0")
      }
    );

    window.diagram = diagram;

    diagram.nodeTemplate = $(
      go.Node,
      "Auto",
      { desiredSize: new go.Size(300, 100) },
      new go.Binding("location", "loc", go.Point.parse),
      // $(go.Shape, "RoundedRectangle", { fill: "lightgray" }),
      $(
        go.TextBlock,
        // { margin: 15 }
        //new go.Binding("text", "key")
      )
    );

    diagram.linkTemplate = $(
      go.Link,
      {
        routing: go.Link.AvoidsNodes,
        corner: 10,
        fromSpot: go.Spot.BottomSide,
        toSpot: go.Spot.TopSide
      },
      $(
        go.Shape, { strokeWidth: 4, stroke: "rgba(173, 173, 173, 0.25)" },
        new go.Binding("strokeWidth", "width")
      )
    );

    function getOffset(el) {
      const rect = el.getBoundingClientRect();
      return {
        left: rect.left + window.scrollX,
        top: rect.top + window.scrollY
      };
    }

    const elements = [...this.$el.querySelectorAll('.phone')];
    const viewport = this.$el.querySelectorAll('#draw-layer')[0];
    const viewPortOffset = getOffset(viewport);

    var nodeDataArray = elements.map((el, index) => {
      const elOffset = getOffset(el);

      return {
        key: index,
        loc: `${elOffset.left - viewPortOffset.left} ${elOffset.top - viewPortOffset.top}`,
      }
    })

    var linkDataArray = [
      { from: "0", to: "1", width: 30 },
      { from: "0", to: "2", width: 50 },
      { from: "2", to: "3", width: 1 },
      { from: "2", to: "4", width: 5 },
      { from: "2", to: "5", width: 40 },
      { from: "2", to: "11", width: 10 },
      { from: "5", to: "6", width: 40},
      { from: "6", to: "7", width: 30},
      { from: "7", to: "8", width: 20},
      { from: "8", to: "9", width: 10},
      { from: "9", to: "10", width: 5 },
    ];
    diagram.model = new go.GraphLinksModel(nodeDataArray, linkDataArray);
  }

  get style() {
    return {
      transform: `scale(${this.scale})`
    };
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
html,
body {
}

.hello {
}

.viewport {
  border: 3px solid black;
  height: calc(100vh - 100px);
  width: 1000px;
  margin: auto;
}

.hello > .wrapper {
  //overflow: auto;
}
</style>
