<template>
<div>
  <upload-list
  action="string"
  :list-type="listType" 
  :files="uploadFiles"
  :handle-preview="onPreview"
  :handle-remove="onRemove"
  >
  </upload-list>
  <div class="el-upload el-upload--picture-card">
    <i class="el-icon-plus"></i>
    <input class="el-upload__input" @change="handleChange" type="file" ></input>
  </div>
</div>

</template>
<script>
import UploadList from './upload-list';
export default {
  props:{
    action: {
      type: String,
      required: true
    },
    listType: {
      type: String,
      default: 'text' // text,picture,picture-card
    },
    fileList: {
      type: Array,
      default() {
        return [];
      }
    },
    onPreview: {
      type: Function
    },
    onRemove:{
      type:Function
    },
    onChange:{
      type:Function
    }
  },
  data(){
    return {
      uploadFiles: [],
      tempIndex: 1
    }
  },
  components:{
    UploadList
  },
  methods:{
    handleChange(e){
      let target = e.target
      this.onChange(target.files[0])
      target.value=""
    }
  },
  watch:{
    listType(type) {
      if (type === 'picture-card' || type === 'picture') {
        this.uploadFiles = this.uploadFiles.map(file => {
          if (!file.url && file.raw) {
            try {
              file.url = URL.createObjectURL(file.raw);
            } catch (err) {
              console.error('[Element Error][Upload]', err);
            }
          }
          return file;
        });
      }
    },
    fileList: {
      immediate: true,
      handler(fileList) {
        this.uploadFiles = fileList.map(item => {
          item.uid = item.uid || (Date.now() + this.tempIndex++);
          item.status = item.status || 'success';
          return item;
        });
      }
    }
  }
}
</script>
<style scoped>
.el-upload--picture-card{
  overflow: hidden;
  position: relative;
}
.el-upload__input{
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  opacity: 0;
  width: 100%;
  height: 100%;
}
</style>


