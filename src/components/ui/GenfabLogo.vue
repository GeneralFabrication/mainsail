<template>
  <img
    src="/img/genfablogow_rotated.png"
    :alt="alt"
    :style="styles"
  />
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class GenfabLogo extends Vue {
  @Prop({ default: '50px' }) readonly size!: string
  @Prop({ default: '#FFFFFF' }) readonly color!: string
  @Prop({ default: 'Genfab Logo' }) readonly alt!: string

  get styles() {
    return {
      width: this.size,
      height: this.size,
      filter: this.color !== '#FFFFFF' ? `brightness(0) saturate(100%) ${this.colorToFilter(this.color)}` : 'none'
    }
  }

  colorToFilter(color: string): string {
    // This is a simple conversion and may not work for all colors
    return `invert(100%) sepia(100%) saturate(10000%) hue-rotate(${this.colorToHue(color)}deg)`
  }

  colorToHue(color: string): number {
    const r = parseInt(color.slice(1, 3), 16)
    const g = parseInt(color.slice(3, 5), 16)
    const b = parseInt(color.slice(5, 7), 16)
    return Math.atan2(Math.sqrt(3) * (g - b), 2 * r - g - b) * (180 / Math.PI)
  }

  mounted() {
    console.log('GenfabLogo mounted, size:', this.size, 'color:', this.color)
  }
}
</script>
