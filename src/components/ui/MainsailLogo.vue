<template>
    <svg
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        x="0px"
        y="0px"
        viewBox="0 0 599.38 523.11"
        xml:space="preserve">
    <use :href="'/img/genfablogo.svg#logo'" />
    </svg>
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

    @Watch('color')
    colorChanged(newVal: string) {
        this.internalColor = newVal !== '' ? newVal : defaultLogoColor
    }

    created() {
        if (this.color !== '') this.internalColor = this.color
    }
}
</script>
