<template>
  <!--当 button 点击后触发当前对象（整个组件）-->
  <button class="b-button" :class="{[`icon-${iconPosition}`]: true}"
          @click="$emit('click')">
    <b-icon class="icon" v-if="icon && !loading" :name="icon"></b-icon>
    <b-icon class="loading icon" v-if="loading" name="loading"></b-icon>
    <div class="content">
      <slot></slot>
    </div>

  </button>
</template>

<script>
  export default {
    // props: ['icon', 'iconPosition']
    props: {
      icon: {},
      loading: {
        type: Boolean,
        default: false
      },
      iconPosition: {
        type: String,
        default: 'left',
        validator(value) {
          return value === 'left' || value === 'right';
        }
      }
    }
  }
</script>

<style lang="scss">
  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .b-button {
    font-size: var(--font-size);
    height: var(--button-height);
    padding: 0 1em;
    border-radius: var(--border-radius);
    border: 1px solid var(--border-color);
    background: var(--button-bg);
    display: inline-flex;
    justify-content: center;
    align-items: center;
    vertical-align: middle;

    &:hover {
      border-color: var(--border-color-hover);
    }

    &:active {
      background-color: var(--button-active-bg);
    }

    &:focus {
      outline: none;
    }

    > .content {
      order: 2;
    }

    > .icon {
      order: 1;
      margin-right: .3em;
    }

    &.icon-right {
      > .content {
        order: 1;
      }

      > .icon {
        order: 2;
        margin-right: 0;
        margin-left: .3em;
      }
    }

    .loading {
      animation: spin 1s infinite linear;
    }
  }
</style>