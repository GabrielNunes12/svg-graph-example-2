<template>
  <section>
    <svg width="500" height="500">
       <path
        class="radial"
        :d="radialData"
        transform="translate(250, 250)"
        fill="green"
      ></path>
    </svg>
    <input name="rays" type="range" max="50" v-model="rays">
  </section>
</template>

<script>
import { lineRadial } from 'd3-shape';
export default {

  data(){
    return{
      outerRadius: 200,
      rays: 5,
    }
  },
  computed: {
    innerRadius(){
      return this.outerRadius * 0.8;
    },
    radialPoints() {
      const step = 2 * Math.PI / (this.rays * 2);
      const points = [];
      for (let i = 0 ; i <= this.rays * 2; i++){
        const currentRadius = i % 2 ? this.innerRadius : this.outerRadius;
        points.push([i * step, currentRadius])
      }
      return points
    },
    radialData(){
      const radialLineGenerator = lineRadial();
      return radialLineGenerator(this.radialPoints);
    }
  }
}
</script>
