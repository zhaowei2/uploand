<template>
  <transition-group
    tag="ul"
    :class="[
      'el-upload-list',
      'el-upload-list--' + listType,
      { 'is-disabled': disabled }
    ]"
    name="el-list"
  >
    <li
      v-for="file in files"
      :class="['el-upload-list__item', 'is-' + file.status, focusing ? 'focusing' : '']"
      :key="file.uid"
      tabindex="0"
    >
      <slot :file="file">
        <img
          class="el-upload-list__item-thumbnail"
          v-if="file.status !== 'uploading' && ['picture-card', 'picture'].indexOf(listType) > -1"
          :src="file.url" alt=""
        >
        <a class="el-upload-list__item-name" @click="handleClick(file)">
          <i class="el-icon-document"></i>{{file.name}}
        </a>
        <label class="el-upload-list__item-status-label">
          <i :class="{
            'el-icon-upload-success': true,
            'el-icon-circle-check': listType === 'text',
            'el-icon-check': ['picture-card', 'picture'].indexOf(listType) > -1
          }"></i>
        </label>
        <!-- 删除 -->
        <i class="el-icon-close" v-if="!disabled" @click="handleClickRemove(file)"></i>
        <!--  -->
        <!-- 预览 -->
        <span class="el-upload-list__item-actions" v-if="listType === 'picture-card'">
          <span
            class="el-upload-list__item-preview"
            v-if="handlePreview && listType === 'picture-card'"
            @click="handlePreview(file)"
          >
            <i class="el-icon-zoom-in"></i>
          </span>
          <span
            v-if="!disabled"
            class="el-upload-list__item-delete"
            @click="handleClickRemove(file)"
          >
            <i class="el-icon-delete"></i>
          </span>
        </span>
      </slot>
    </li>  
  </transition-group>
</template>
<script>
export default {
  name: 'ElUploadList',
  
  props:{
    files: {
      type: Array,
      default() {
        return [];
      }
    },
    disabled: {
      type: Boolean,
      default: false
    },
    listType: String,
    handleRemove:Function,
    handlePreview: Function,
    // handleRemove:Function
  },
  data(){
    return {
      focusing: false
    };
  },
  methods:{
    handleClick(file) {
      this.handlePreview && this.handlePreview(file);
    },
    handleClickRemove(file){
      this.handleRemove && this.handleRemove(file)
    }
  }
}
</script>

