<template>
   <uploadBox></uploadBox>
   <div class="pdf-box">
       <div class="pdf_down" >
            <div class="pdf_set_left"  @click="scaleD()">放大</div>
            <div class="pdf_set_middle" @click="scaleX()">缩小</div>
        </div>

        <div :style="{width:pdf_div_width,margin:'0 auto'}" >
            <canvas v-for="page in pdf_pages" :id="'the-canvas'+page" :key="page"></canvas>
        </div>
   </div>
</template>
<script>
import uploadBox from '../upload.vue';
// let PDFJS = require('pdfjs-dist');
import * as PdfJs from 'pdfjs-dist/legacy/build/pdf.js' // 注意导入的写法
// import PDFJS from 'pdfjs-dist';
console.log(PDFJS)
export default{
    components:{
        uploadBox
    },
    data(){
        return{
            pdf_scale:1.0,//pdf放大系数
            pdf_pages:[],
            pdf_div_width:'',
            pdf_src:null,
        }
    },
    methods:{
        _loadFile (url) {  //初始化pdf
            let loadingTask = PDFJS.getDocument(url)
            loadingTask.promise
            .then((pdf) => {
            this.pdfDoc = pdf
            this.pdf_pages = this.pdfDoc.numPages
            this.$nextTick(() => {
                this._renderPage(1)
            })
            })
        },
        get_pdfurl(){  //获得pdf
        //例子:加载pdf线上示例
         this.pdf_src = 'https://mozilla.github.io/pdf.js/web/compressed.tracemonkey-pldi-09.pdf'
         this._loadFile(this.pdf_src)
           return

           //线上请求
         this.$axios.get('')
         .then((res)=>{
            this.pdf_src = res.url
            this._loadFile(this.pdf_src)
         })
     }
    },
    mounted(){
        this.get_pdfurl()
    }
}
</script>