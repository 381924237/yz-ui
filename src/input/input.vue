<template>
  <div class="wrapper" :class="{error}">
    <input type="text" :value="value" :disabled="disabled" :readonly="readonly" 
      @change="$emit('change',$event.target.value)"
      @input="$emit('input',$event.target.value)"
      @focus="$emit('focus',$event.target.value)"
      @blur="$emit('blur',$event.target.value)"      
    >
    <template v-if="error">
      <Icon name="error" class="icon-error"></Icon>
      <span class="errorMessage">{{error}}</span>
    </template>
  </div>
</template>

<script>
import Icon from '../icon/icon'

export default {
  name: 'yInput',
  components: {
    Icon
  },
  props: {
    value: {
      type: String
    },
    disabled: {
      type: Boolean,
      default: false
    },
    readonly: {
      type: Boolean,
      default: false
    },
    error: {
      type: String
    }
  }
}

</script>

<style lang='scss' scoped>
  $border-size: 2px;
  $height: 32px;
  $border-color: #999;
  $border-color-hover: rgb(0, 179, 134);
  $border-radius: 4px;
  $font-size: 12px; 
  $box-shadow-color: rgba(0,0,0,0.5);
  $red: #F1453D;
  .wrapper{
    font-size: $font-size;
    display: inline-flex;
    align-items: center;
    > :not(:last-child){
      margin-right: 0.5em;
    }
    > input{
      height: $height;
      border: $border-size solid $border-color;
      border-radius: $border-radius;
      padding: 0 8px;
      font-size: inherit;
      &:hover{
        border-color: $border-color-hover; 
      }
      &:focus{
        border-color: $border-color-hover;
        outline: none;
      }
      &[disabled], &[readonly]{
        border-color: #ccc;
        color: #ccc; 
        cursor: not-allowed;
        background-color: #fff;
      }
    }
    &.error{
    > input{
      border-color: $red;
    }
    .icon-error {
      fill: $red;
    }
    .errorMessage{
      color: $red;
    }
    }
  }
</style>