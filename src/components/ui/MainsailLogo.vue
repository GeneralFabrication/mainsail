<template>
  <div :style="containerStyle">
    <img
      src="/img/genfablogow_rotated.png"
      alt="Mainsail Logo"
      :style="logoStyle"
    />
  </div>
</template>

<script lang="ts">
import Component from 'vue-class-component'
import { Mixins, Prop, Watch } from 'vue-property-decorator'
import BaseMixin from '../mixins/base'
import { defaultLogoColor } from '@/store/variables'

@Component
export default class MainsailLogo extends Mixins(BaseMixin) {
  private internalColor = defaultLogoColor

  @Prop({ required: false, default: '' })
  declare readonly color: string

  @Prop({ required: false, default: '100%' })
  declare readonly width: string

  @Prop({ required: false, default: '0px' })
  declare readonly marginTop: string

  @Watch('color')
  colorChanged(newVal: string) {
    this.internalColor = newVal !== '' ? newVal : defaultLogoColor
  }

  created() {
    if (this.color !== '') this.internalColor = this.color
  }

  get containerStyle() {
    return {
      width: this.width,
      display: 'inline-block',
      marginTop: this.marginTop,
    }
  }

  get logoStyle() {
    return {
      width: '100%',
      height: 'auto',
      display: 'block',
      filter: this.internalColor !== defaultLogoColor ? this.colorToFilter(this.internalColor) : 'none'
    }
  }

  colorToFilter(color: string): string {
    return `brightness(0) saturate(100%) ${this.colorToRGB(color)}`
  }

  colorToRGB(color: string): string {
    const r = parseInt(color.slice(1, 3), 16)
    const g = parseInt(color.slice(3, 5), 16)
    const b = parseInt(color.slice(5, 7), 16)
    return `invert(${r/255*100}%) sepia(${g/255*100}%) saturate(${b/255*100}%)`
  }
}
</script>
