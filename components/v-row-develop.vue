<template>
  <div>
    <p contenteditable="true" ref="sas">asdasdasd</p>
      <div class="DevRow">
        <button  class="btnD BackAct" @click="Undo">
          <img id="backActImg" src="../assets/VectorBackAct.png" alt="">
        </button>
        <button class="btnD RepeatAct"  @click="Redo">
          <img class="RepeatActImg" src="../assets/VectorRepeatAct.png" alt="">
        </button>
        <button class="btnD TitleT" @click="ToHead">
          <img class="TitleImg" src="../assets/VectorTitleT.png" alt="">
        </button>
        <button @click="ToParagraph" class="btnD Paragraph">
          <img class="ParagraphImg1" src="../assets/VectorParagraph.png" alt="">
          <img class="ParagraphImg2" src="../assets/VectorParagraph.png" alt="">
        </button>
        <button @click="PasteImgM" class="btnD PasteImgBlock">
          <img class="PasteImg" src="../assets/VectorPasteImg.png" alt="">
        </button >
        <a  v-clipboard="htmlcodea" @click="CopyHtml" class="CopyHtml" href="#">
          Скопировать HTML
        </a>
      </div>
      <HtmlCode @myEvent="DoSomthing($event)"/>
      <div class="TextAreaBlock">
        <div ref="txtarea" class="textArea" >
          <p id="area" ref="TextP" class="BordenUp" contenteditable="true"> {{ttt}} </p>
        </div>
      </div>
  </div>
</template>

<script>
import HtmlCode from '../components/HtmlCode'
export default {
  mounted () {
    this.text = this.$refs.PText
  },
  data () {
    return {
      htmlcodea: '<!DOCTYPE html> <html lang="en">  <head>    <meta charset="utf-8">    <meta http-equiv="X-UA-Compatible" content="IE=edge">    <meta name="viewport" content="width=device-width,initial-scale=1.0">    <link rel="icon" href="<%= BASE_URL %>favicon.ico">    <title><%= htmlWebpackPlugin.options.title %></title>  </head>  <body>    <noscript>      <strong>Were sorry but <%= htmlWebpackPlugin.options.title %> doesn t work properly without JavaScript enabled. Please enable it to continue.</strong>    </noscript>    <div id="app"></div>    <!-- built files will be auto injected -->  </body></html>)',
      start: 0,
      end: 0,
      ttt: 'Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.'
    }
  },
  components: {
    HtmlCode
  },
  methods: {
    DoSomthing (alph) {
      this.htmlcodea = alph
      console.log(this.htmlcodea)
    },
    CopyHtml () {
      return this.htmlcode
    },
    PasteImgM () {
      const a = prompt()
      this.$refs.txtarea.focus()
      if (a !== null) {
        document.execCommand('insertImage', false, a)
      }
    },
    Undo () {
      this.$refs.txtarea.focus()
      document.execCommand('undo')
    },
    Redo () {
      this.$refs.txtarea.focus()
      document.execCommand('redo')
      console.log(document.execCommand(this.$refs.TextP.innerHTML))
    },
    ToHead () {
      var range = window.getSelection().getRangeAt(0)
      const seltext = document.getSelection().toString().trim()
      const stext = (this.$refs.TextP.textContent.substring(0, range.startOffset) + '<h2>' + seltext + '</h2>' + this.$refs.TextP.innerHTML.substring(range.endOffset))
      this.$refs.TextP.innerHTML = stext
    },
    ToParagraph () {
      var range = window.getSelection().getRangeAt(0)
      const seltext = document.getSelection().toString().trim()
      this.$refs.txtarea.focus()
      const stext = (this.$refs.TextP.textContent.substring(0, range.startOffset) + '<span style="white-space: pre-wrap;"> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>' + seltext + '<br>' + this.$refs.TextP.innerHTML.substring(range.endOffset))
      this.$refs.TextP.innerHTML = stext
      console.log(this.$refs.TextP.textContent.substring(range.startOffset, range.endOffset))
      // Я делал механику параграфа 8 часов!
    }
  }
}
</script>

<style>
.btnD:active, .btnD:focus{
outline-color: rgb(20, 96, 211);
}
img{
  transform: translate(10%);
  display: block;
}
.BordenUp:active, .BordenUp:focus {
  outline-color: #639EFF;
  border-color: #639EFF;
}
.textArea{
  min-height: 984px;;
  border: none;
  font-family: 'Roboto', sans-serif;
  border-color: rgb(48, 44, 44) ;
  width: 746px;
  background-color: #282828;
  color: white;
}
.TextAreaBlock{
position: absolute;
width: 621px;
height: 253px;
left: 107px;
top: 146px;

font-family: Roboto;
font-style: normal;
font-weight: normal;
font-size: 15px;
line-height: 23px;
/* or 153% */
color: #EAEAEA;
}
.CopyHtml{
position: absolute;
width: 137px;
height: 23px;
left: 384px;
top: 85px;
font-family: 'Roboto', sans-serif;
font-style: normal;
font-weight: normal;
font-size: 15px;
line-height: 23px;
color: #639EFF;
}
.PasteImg{
position: absolute;
left: 25.69%;
right: 50.02%;
top: 24.22%;
bottom: 92.35%;
}
.PasteImgBlock{
border:none;
position: absolute;
width: 42px;
height: 38px;
left: 323px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.ParagraphImg1{
  position: absolute;
left: 18.14%;
right: 51.83%;
top: 28.79%;
bottom: 21.65%;
}
.ParagraphImg2{
position: absolute;
left: 50.11%;
right: 3.86%;
top: 28.79%;
bottom: 21.65%;
}
.Paragraph{
  border: none;
  position: absolute;
width: 42px;
height: 38px;
left: 269px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.TitleImg{
  position: absolute;
left: 26.19%;
right: 87.54%;
top: 20.29%;
bottom: 92.27%;
}
.TitleT{
  border: none;
  position: absolute;
width: 42px;
height: 38px;
left: 215px;
top: 77px;

background: #282828;
border-radius: 4px;
}
#backActImg{
  position: absolute;
left: 20.19%;
right: 85.54%;
top: 20.29%;
bottom: 92.27%;

}
.BackAct{
  border: none;
  position: absolute;
width: 42px;
height: 38px;
left: 107px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.RepeatAct{
  border: none;
position: absolute;
width: 42px;
height: 38px;
left: 161px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.RepeatActImg{
  position: absolute;
left: 20.09%;
right: 77.64%;
top: 20.29%;
bottom: 92.27%;

}
</style>
