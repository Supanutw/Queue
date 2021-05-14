<template>
  <h1>รับคิว</h1>
  <div id="container"></div>
  <img id="canvas" />

</template>

<script>
import QRCode from "qrcode";
import Instascan from "instascan";
// import Swal from 'sweetalert2'

QRCode.toDataURL(new Date())
  .then((url) => {
    return url;
  })
  .catch((err) => {
    return err;
  });

// var opts = {
//   errorCorrectionLevel: "H",
//   type: "image/jpeg",
//   quality: 0.3,
//   margin: 1,
//   color: {
//     dark: "#010599FF",
//     light: "#FFBF60FF",
//   },
// };
// let segs = [
//   { data: "I am a ICE 🍻🧑‍💻", mode: "Kanji" },
//   { data: "http://localhost:8081/bookingsuccess", mode: "Kanji" },
// ];

export default {
  setup() {
    const generateQR = async (text) => {
      try {
        return await QRCode.toDataURL(text);
      } catch (err) {
        return err;
      }
    };
    generateQR(new Date().toString()).then((res) => {
      var img = document.getElementById("canvas");
      img.src = res;
    });
  
    return {
      generateQR,
    };
  },
  methods() {},

  mounted() {
    // QRCode.toCanvas(segs, opts, function (err, canvas) {
    //   if (err) throw err;
    //   var container = document.getElementById("container");
    //   container.appendChild(canvas);
    //   console.log(container);
    // });
     let scanner = new Instascan.Scanner({ video: document.getElementById('preview') });
      scanner.addListener('scan', function (content) {
        console.log(content);
        alert(content)
      });

      // Instascan.Camera.getCameras().then(function (cameras) {
      //   console.log(cameras)
      //   scanner.start(cameras[0]);
      //   // if (cameras.length > 0) {
      //   //   console.log(document.getElementById('preview'))
      //   //   scanner.start(cameras[0]);
      //   // } else {
      //   //   console.error('No cameras found.');
      //   // }
      // }).catch(function (e) {
      //   console.error(e);
      // });
  },
};
</script>

<style>
</style>