<template>
  <button
    :class="[
      'button',
      type && `button-${type}`,
      size && size !== 'default' && `button-${size}`,
      plain && 'is-plain',
      round && 'is-round',
      circle && 'is-circle',
      disabled && 'is-disabled',
      text && 'is-text',
      loading && 'is-loading',
    ]"
    :type="htmlType"
    :autofocus="autofocus"
    :disabled="disabled || loading"
    @click="handleClick"
  >
    <i v-if="loading" class="icon-loading" />
    <i v-if="!loading && icon" :class="`icon-${icon}`" />
    <span v-if="$slots.default">
      <slot />
    </span>
  </button>
</template>

<script lang="ts">
import { Vue, Component, Prop, Emit } from 'vue-property-decorator';

@Component({
  name: 'Button',
})
export default class Button extends Vue {
  // type
  @Prop({
    type: String,
    required: false,
    default: 'primary',
    validator(value) {
      return ['primary', 'danger'].indexOf(value) !== -1;
    },
  })
  private readonly type!: string;

  // html type
  @Prop({
    type: String,
    required: false,
    default: 'button',
    validator(value) {
      return ['button', 'reset', 'submit'].indexOf(value) !== -1;
    },
  })
  private readonly htmlType!: string;

  // size
  @Prop({
    type: String,
    required: false,
    default: 'default',
    validator(value) {
      return ['small', 'default', 'large'].indexOf(value) !== -1;
    },
  })
  private readonly size!: string;

  // plain
  @Prop({
    type: Boolean,
    required: false,
    default: false,
  })
  private readonly plain!: boolean;

  // round
  @Prop({
    type: Boolean,
    required: false,
    default: false,
  })
  private readonly round!: boolean;

  // circle
  @Prop({
    type: Boolean,
    required: false,
    default: false,
  })
  private readonly circle!: boolean;

  // text
  @Prop({
    type: Boolean,
    required: false,
    default: false,
  })
  private readonly text!: boolean;

  // disabled
  @Prop({
    type: Boolean,
    required: false,
    default: false,
  })
  private readonly disabled!: boolean;

  // loading
  @Prop({
    type: Boolean,
    required: false,
    default: false,
  })
  private readonly loading!: boolean;

  // icon
  @Prop({
    type: String,
    required: false,
  })
  private readonly icon!: string;

  // autofocus
  @Prop({
    type: Boolean,
    required: false,
    default: false,
  })
  private readonly autofocus!: boolean;

  // event emit
  @Emit()
  private click(e: MouseEvent): MouseEvent {
    return e;
  }

  // handle button click event
  private handleClick(e: MouseEvent): void {
    // emit
    if (this.$listeners.click) {
      this.click(e);
    }
  }
}
</script>

<style lang="scss">
@import './Button.scss';
</style>
