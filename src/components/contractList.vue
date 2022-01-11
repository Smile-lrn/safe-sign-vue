<template>
    <div :style="{ width: pdf_div_width, margin: '0 auto' }">
        <canvas v-for="page in pdf_pages" :id="'pdfCanvas_' + page" :key="page"></canvas>
    </div>
</template>
<script  >
import * as PdfJs from 'pdfjs-dist/legacy/build/pdf.js'
import pdfjsWorker from 'pdfjs-dist/build/pdf.worker.entry';
import { getDocument, GlobalWorkerOptions } from 'pdfjs-dist'
GlobalWorkerOptions.workerSrc = pdfjsWorker


export default {
    data() {
        return {
            pdf: 'https://mozilla.github.io/pdf.js/web/compressed.tracemonkey-pldi-09.pdf',
            pdf_scale: 1.0,//pdf放大系数
            pdf_pages: [],
            pdf_div_width: '',
            pdf_src: null,
            pdfDoc: ''
        }
    },
    methods: {
        loadFile(url) {
            // 设定pdfjs的 workerSrc 参数
            // NOTE: 这一步要特别注意，网上很多关于pdfjs的使用教程里漏了这一步，会出现workerSrc未定义的错误
            // PdfJs.GlobalWorkerOptions.workerSrc = pdfWorker;

            let loadingTask = getDocument(url)
            loadingTask.promise
                .then((pdf) => {
                    this.pdfDoc = pdf
                    this.pdf_pages = this.pdfDoc.numPages
                    this.$nextTick(() => {
                        this.renderPage(this.pdf_pages,pdf)
                    })
                })
        },

        // num 表示渲染第几页
        renderPage(num,pdf) {
            pdf.getPage(num).then((page) => {
                console.log(num,page)
                const canvas = document.getElementById('pdfCanvas_'+page._pageIndex) // 获取页面中的canvas元素
                // 以下canvas的使用过程
                const ctx = canvas.getContext('2d')
                const dpr = window.devicePixelRatio || 1
                const bsr = ctx.webkitBackingStorePixelRatio ||
                    ctx.mozBackingStorePixelRatio ||
                    ctx.msBackingStorePixelRatio ||
                    ctx.oBackingStorePixelRatio ||
                    ctx.backingStorePixelRatio ||
                    1
                const ratio = dpr / bsr
                const viewport = page.getViewport({ scale: this.pdfScale }) // 设置pdf文件显示比例
                canvas.width = viewport.width * ratio
                canvas.height = viewport.height * ratio
                canvas.style.width = viewport.width + 'px'
                canvas.style.height = viewport.height + 'px'
                ctx.setTransform(ratio, 0, 0, ratio, 0, 0) // 设置当pdf文件处于缩小或放大状态时，可以拖动
                const renderContext = {
                    canvasContext: ctx,
                    viewport: viewport
                }
                // 将pdf文件的内容渲染到canvas中
                page.render(renderContext)
            })
        }
    },
    mounted() {
        this.loadFile(this.pdf)
    }
}
</script>
