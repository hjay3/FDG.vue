<template>
  <div ref="graphContainer"></div>
</template>

<script>
import ForceGraph3D from '3d-force-graph';

export default {
  name: 'ForceGraphComponent',
  data() {
    return {
      graph: null,
      // Sample data - you can replace this with your actual data
      myGraphData: {
        nodes: [
          { id: 1, name: 'Node 1', color: '#ff0000' },
          { id: 2, name: 'Node 2', color: '#00ff00' },
          { id: 3, name: 'Node 3', color: '#0000ff' },
          { id: 4, name: 'Node 3', color: '#0000ff' },
          { id: 5, name: 'Node 3', color: '#0000ff' },
        ],
        links: [
          { source: 1, target: 2 },
          { source: 2, target: 3 },
          { source: 1, target: 3 },
        ],
      },
    };
  },
  mounted() {
    this.initGraph();
  },
  methods: {
    initGraph() {
      this.graph = ForceGraph3D()(this.$refs.graphContainer)
        .graphData(this.myGraphData)
        .nodeLabel('name')
        .nodeColor((node) => node.color)
        .nodeRelSize(18) // Increase node size
        .linkWidth(12)
        .linkOpacity(0.8)
        .backgroundColor('#f0f0f0') // Light gray background
        .width(this.$refs.graphContainer.offsetWidth)
        .height(600)
        // Add some spacing between nodes
        .d3Force('charge', d3.forceManyBody().strength(-350))
        // Enable camera controls
        .enableNavigationControls(true)
        .showNavInfo(true);
    },
  },
  beforeUnmount() {
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
  border: 1px solid #ccc;
}
</style>
