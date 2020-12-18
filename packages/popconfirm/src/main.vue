<template>
  <el-popover
    v-bind="$attrs"
    v-model="visible"
    trigger="click"
  >
  <div class="el-popconfirm">
    <p class="el-popconfirm__main">
    <i
      v-if="!hideIcon"
      :class="icon"
      class="el-popconfirm__icon"
      :style="{color: iconColor}"
    ></i>
      {{title}}
    </p>
    <div class="el-popconfirm__action">
      <el-button 
        size="mini" 
        :type="cancelButtonType" 
        @click="cancel"
      >
        {{typeof cancelButtonText !== 'undefined' ? cancelButtonText : t('el.popconfirm.cancelButtonText')}}
      </el-button>
      <el-button 
        size="mini" 
        :type="confirmButtonType" 
        @click="confirm"
      >
        {{typeof confirmButtonText !== 'undefined' ? confirmButtonText : t('el.popconfirm.confirmButtonText')}}
      </el-button>
    </div>
  </div>
  <slot name="reference" slot="reference"></slot>
</el-popover>
</template>

<script>
import ElPopover from 'element-ui/packages/popover';
import ElButton from 'element-ui/packages/button';
import Locale from 'element-ui/src/mixins/locale';

export default {
  name: 'ElPopconfirm',
  mixins: [Locale],
  props: {
    title: {
      type: String
    },
    confirmButtonText: String,
    cancelButtonText: String,
    confirmButtonType: {
      type: String,
      default: 'primary'
    },
    cancelButtonType: {
      type: String,
      default: 'text'
    },
    icon: {
      type: String,
      default: 'el-icon-question'
    },
    iconColor: {
      type: String,
      default: '#f90'
    },
    hideIcon: {
      type: Boolean,
      default: false
    }
  },
  components: {
    ElPopover,
    ElButton
  },
  data() {
    return {
      visible: false
    };
  },
  methods: {
    confirm() {
      this.visible = false;
      this.$emit('onConfirm');
    },
    cancel() {
      this.visible = false;
      this.$emit('onCancel');
    }
  }
};
</script>
