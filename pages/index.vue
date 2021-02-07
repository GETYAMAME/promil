<template>
  <div>
    <p><canvas id="preview"></canvas></p>
    <p>
      <input type="text" id="canvas_text" value="我輩は犬である">
      <button @click="drawText('preview', 'canvas_text');">文字を描く</button>
      <button @click="load();">画像を読み込む</button>
    </p>
  </div>
</template>

<script>
export default {
 methods: {
   upload(){
    var reader = new FileReader();
    reader.onload = function (e) {
        $("#preview").attr('src', e.target.result);
    }
    reader.readAsDataURL(e.target.files[0]);
   },
   load () {
      //画像を読み込んでImageオブジェクトを作成する
      var image = new Image();
      image.src = 'canva.jpg';
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

