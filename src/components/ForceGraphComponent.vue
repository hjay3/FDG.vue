<template>
  <div ref="graphContainer"></div>
</template>

<script>
//import ForceGraph from 'force-graph'; // or import ForceGraph3D from '3d-force-graph'
import ForceGraph3D from '3d-force-graph';

export default {
  name: 'ForceGraphComponent',
  data() {
    return {
      graph: null,
    };
  },
  props: {
    graphData: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    this.initGraph();
  },
  methods: {
    initGraph() {
      this.graph = ForceGraph()(this.$refs.graphContainer)
        .graphData(this.graphData)
        .nodeId('id')
        .nodeLabel('name')
        .nodeColor('color')
        .linkSource('source')
        .linkTarget('target')
        .width(this.$refs.graphContainer.offsetWidth)
        .height(600);
    },
  },
  watch: {
    graphData: {
      handler(newData) {
        if (this.graph) {
          this.graph.graphData(newData);
        }
      },
      deep: true,
    },
  },
  beforeDestroy() {
    if (this.graph) {
      this.graph._destructor();
    }
  },
};
</script>

<style scoped>
div {
  width: 100%;
  height: 600px;
}
</style>
