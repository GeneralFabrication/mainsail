<template>
  <svg :width="size" :height="size" :style="{ fill: color }">
    <use :href="'/img/genfablogo.svg#logo'" />
  </svg>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class GenfabLogo extends Vue {
  @Prop({ default: '50px' }) readonly size!: string
  @Prop({ default: '#FFFFFF' }) readonly color!: string

  mounted() {
    console.log('GenfabLogo mounted, size:', this.size, 'color:', this.color)
  }
}
</script>
