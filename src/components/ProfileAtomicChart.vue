<template>
  <div class="pachart" ref="chartdiv"></div>
</template>

<script>
import * as am5 from '@amcharts/amcharts5';
import * as am5hierarchy from '@amcharts/amcharts5/hierarchy';
import am5themes_Animated from '@amcharts/amcharts5/themes/Animated';

import { data as PAData } from '../data/pachart.data.js';

export default {
  name: 'ProfileAtomicChart',
  mounted() {
    let root = am5.Root.new(this.$refs.chartdiv);

    root.setThemes([am5themes_Animated.new(root)]);

    let data = PAData;

    // Create wrapper container
    let container = root.container.children.push(
      am5.Container.new(root, {
        width: am5.percent(100),
        height: am5.percent(100),
        layout: root.verticalLayout,
      })
    );

    // Create series
    // https://www.amcharts.com/docs/v5/charts/hierarchy/#Adding
    let series = container.children.push(
      am5hierarchy.ForceDirected.new(root, {
        singleBranchOnly: false,
        downDepth: 2,
        topDepth: 1,
        initialDepth: 1,
        valueField: 'value',
        categoryField: 'name',
        childDataField: 'children',
        idField: 'name',
        linkWithField: 'linkWith',
        manyBodyStrength: -10,
        centerStrength: 0.8,
      })
    );

    series.get('colors').setAll({
      step: 2,
    });

    series.links.template.set('strength', 0.5);

    series.data.setAll([data]);

    series.set('selectedDataItem', series.dataItems[0]);

    // Make stuff animate on load
    series.appear(1000, 100);

    this.root = root;
  },

  beforeDestroy() {
    if (this.root) {
      this.root.dispose();
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pachart {
  width: 600px;
  max-width: 100%;
  height: 600px;
}
</style>
