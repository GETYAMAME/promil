<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <center>
        <h1>Nuxt.js + uppy example</h1>
        <v-btn id="select-files" color="primary">upload</v-btn>
      </center>
    </v-flex>
  </v-layout>
</template>

<script>
import Uppy from '@uppy/core'
import XHRUpload from '@uppy/xhr-upload'
import Dashboard from '@uppy/dashboard'
import Webcam from '@uppy/webcam'
export default {
  data() {
    return {
      uppyId: 'uppy-trigger'
    }
  },
  mounted() {
    const uppy = Uppy()
      .use(Dashboard, {
        trigger: '#select-files'
      })
      .use(Webcam, { target: Dashboard }) // ウェブカメラを追加
      .use(XHRUpload, { endpoint: 'https://api2.transloadit.com' }) // ダミーのURLへアップロード
    uppy.on('complete', result => {
      // eslint-disable-next-line no-console
      console.log(
        'Upload complete! We’ve uploaded these files:',
        result.successful
      )
    })
  },
  methods: {
    upload(e){
      const file = e.target.files[0]
      const reader = new FileReader()
      reader.onload = (e) => {
        this.generateImgUrl(e.target.result)
      }
      reader.readAsDataURL(file)
    },
    load () {
      var image = new Image();
      image.src = './canva.jpg';
      image.onload = (function () {
        //画像ロードが完了してからキャンバスの準備をする
        var canvas = document.getElementById("preview");
        var ctx = canvas.getContext('2d');
        //キャンバスのサイズを画像サイズに合わせる
        canvas.width = image.width;
        canvas.height = image.height;
        //キャンバスに画像を描画（開始位置0,0）
        ctx.drawImage(image, 0, 0);
      });
    },
    drawText (canvas_id,text_id) {
      var canvas = document.getElementById(canvas_id);
      var ctx = canvas.getContext('2d');
      var text = document.getElementById(text_id);
      //文字のスタイルを指定
      ctx.font = '32px serif';
      ctx.fillStyle = '#404040';
      //文字の配置を指定（左上基準にしたければtop/leftだが、文字の中心座標を指定するのでcenter
      ctx.textBaseline = 'center';
      ctx.textAlign = 'center';
      //座標を指定して文字を描く（座標は画像の中心に）
      var x = (canvas.width / 2);
      var y = (canvas.height / 2);
      ctx.fillText(text.value, x, y);
    },
  },
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

