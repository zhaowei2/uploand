<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <index-html
        action="string"
        list-type="picture-card" 
        :file-list="detailLists"
        :on-preview="handlePreviewGoodsHome"
        :on-remove="handleRemove"
        :on-change="changeUpload"
    >
    </index-html>
  </div>
</template>
<script>
import IndexHtml from './index'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      detailLists:[
        {
          name:'jpg',
          url:'https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3300305952,1328708913&fm=27&gp=0.jpg'
        }
      ],
      img:1
    }
  },
  components: {
    IndexHtml
  },
  methods:{
    handlePreviewGoodsHome(file){
      console.log(file)
      this.img = 1
      console.log('hendpreview')
    },
    handleRemove(file){
      console.log(file)
      console.log('handremove')
    },
    changeUpload(file){
      console.log('changeFile')
      console.log(file)
      this.detailLists.push(file)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
