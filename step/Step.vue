<template>
    <div ref="step" class="c-step">
        <div
            v-for="(item, index) in data"
            :key="'c-step-item' + index"
            class="c-step-item"
            :style="{
                marginLeft:
                    index === 0
                        ? '0'
                        : -Math.ceil((getArrowWidth + 4) / 2) - 1 + 'px',
                width: stepItemWidth + 'px'
            }"
            @click="stepItemClick"
            @mouseover="changeHover(item, true)"
            @mouseleave="changeHover(item, false)"
        >
            <div
                class="c-step-arrow"
                :style="{
                    width: getArrowWidth + 'px',
                    height: getArrowWidth + 'px',
                    backgroundColor:
                        item.hover || item.key === value.key
                            ? heightColor
                            : normalColor,
                    border: arrowWidth + 'px solid' + arrowColor,
                    right:
                        Math.ceil(Math.abs((getArrowWidth - stepHeight) / 2)) +
                        'px'
                }"
            ></div>
            <div
                class="c-step-item-content"
                :style="{
                    backgroundColor:
                        item.hover || item.key === value.key
                            ? heightColor
                            : normalColor,
                    width:
                        stepItemWidth -
                        Math.ceil(getArrowWidth / 2) -
                        10 +
                        'px',
                    paddingLeft:
                        index === 0
                            ? '10px'
                            : Math.ceil(getArrowWidth / 2) + 10 + 'px',
                    lineHeight: stepHeight + 'px',
                    color: textColor
                }"
            >
                {{ item.value }}
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';

interface StepItem {
    value: string;
    key: number;
    hover?: boolean;
}

@Component({})
export default class Step extends Vue {
    @Prop({
        default: (): StepItem[] => {
            return [];
        }
    })
    public data!: StepItem[];
    @Prop({
        default: (): StepItem => {
            return { key: -1, value: '' };
        }
    })
    public value!: StepItem;
    @Prop({ default: '#42b983' })
    public normalColor!: string;
    @Prop({ default: '#229963' })
    public heightColor!: string;
    @Prop({ default: '#fff' })
    public arrowColor!: string;
    @Prop({ default: 4 })
    public arrowWidth!: number;
    @Prop({ default: 150 })
    public stepItemWidth!: number;
    @Prop({ default: '#fff' })
    public textColor!: string;

    private stepHeight: number = 32;
    public mounted(): void {
        // 获取当前step的高度
        if (this.$refs.step) {
            this.stepHeight =
                (this.$refs.step as HTMLDivElement).offsetHeight || 32;
        }
    }

    get getArrowWidth(): number {
        return Math.ceil(Math.sqrt((this.stepHeight * this.stepHeight) / 2));
    }

    private changeHover(item: StepItem, hover: boolean) {
        if (item.hover === undefined) {
            this.$set(item, 'hover', hover);
        } else {
            item.hover = hover;
        }
    }

    private stepItemClick(item: StepItem) {
        this.$emit('input', item);
        this.$emit('stepClick', item);
    }
}
</script>

<style>
.c-step {
    width: auto;
    height: 100%;
    position: relative;
    box-sizing: border-box;
    display: inline-block;
    overflow: hidden;
}
.c-step-item {
    height: 100%;
    float: left;
    position: relative;
    cursor: pointer;
}
.c-step-item-content {
    height: 100%;
    box-sizing: border-box;
    font-size: 14px;
    padding-right: 10px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
.c-step-arrow {
    border-bottom: none !important;
    border-left: none !important;
    position: absolute;
    right: 0;
    z-index: 10;
    top: 50%;
    transform: translateY(-50%) rotate(45deg);
    -ms-transform: translateY(-50%) rotate(45deg); /* IE 9 */
    -moz-transform: translateY(-50%) rotate(45deg); /* Firefox */
    -webkit-transform: translateY(-50%) rotate(45deg); /* Safari 和 Chrome */
    -o-transform: translateY(-50%) rotate(45deg); /* Opera */
}
</style>
