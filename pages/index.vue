<template>
  <div style="max-height: 100%; overflow: auto;">
    <section class="wrapper">
      <LoadingBar/>
      <div
        class="container"
        style="
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
        "
      >
        <div id="scene" class="scene" data-hover-only="false">
          <div class="circle" data-depth="1.2"></div>
          <div class="one" data-depth="0.9">
            <div class="content">
              <span class="piece"></span>
              <span class="piece"></span>
              <span class="piece"></span>
            </div>
          </div>
          <div class="two" data-depth="0.60">
            <div class="content">
              <span class="piece"></span>
              <span class="piece"></span>
              <span class="piece"></span>
            </div>
          </div>
          <div class="three" data-depth="0.40">
            <div class="content">
              <span class="piece"></span>
              <span class="piece"></span>
              <span class="piece"></span>
            </div>
          </div>
          <p class="pcenter" data-depth="0.50">Resonance</p>
          <p class="pcenter" data-depth="0.10">Resonance</p>
        </div>
        <div class="text">
          <article>
            <p>
              Hello, I'm a developer.<br />Make sure to check out the work tab!
            </p>
          </article>
        </div>
      </div>
    </section>
  </div>
</template>
<script setup lang="ts">
import { useHead } from "#imports";
useHead({
  script: [
    {
      src: "https://cdnjs.cloudflare.com/ajax/libs/parallax/3.1.0/parallax.min.js",
      defer: true,
    },
  ],
});

onMounted(() => {
  const scene = document.getElementById('scene');
  if (!scene) {
    console.error('Error: The element with ID "scene" was not found.');
    return;
  }
  const parallax = new Parallax(scene);
});
</script>
<style>
.pcenter {
  font-size: clamp(3.8rem, 8vw, 100rem) !important;
}

@media (max-width: 768px) {
  .pcenter {
    font-size: clamp(3.8, 15rem, 100rem) !important;
  }
}
.wrapper {
  background-color: #3c3f58;
  display: grid;
  grid-template-columns: 1fr;
  justify-content: center;
  align-items: center;
  height: 100vh;
  overflow: hidden;
}
.wrapper .container {
  margin: 0 auto;
  transition: all 0.4s ease;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
.wrapper .container .scene {
  position: absolute;
  width: 100vw;
  height: 100vh;
  vertical-align: middle;
}
.wrapper .container .one,
.wrapper .container .two,
.wrapper .container .three,
.wrapper .container .circle,
.wrapper .container .pcenter {
  width: 60%;
  height: 60%;
  top: 20% !important;
  left: 20% !important;
  min-width: 400px;
  min-height: 400px;
}
.wrapper .container .one .content,
.wrapper .container .two .content,
.wrapper .container .three .content,
.wrapper .container .circle .content,
.wrapper .container .pcenter .content {
  width: 600px;
  height: 600px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.wrapper .container .one .content .piece,
.wrapper .container .two .content .piece,
.wrapper .container .three .content .piece,
.wrapper .container .circle .content .piece,
.wrapper .container .pcenter .content .piece {
  width: 200px;
  height: 80px;
  display: flex;
  position: absolute;
  border-radius: 80px;
  z-index: 1;
  animation: pieceLeft 8s cubic-bezier(1, 0.06, 0.25, 1) infinite both;
}
@keyframes pieceLeft {
  50% {
    left: 80%;
    width: 10%;
  }
}
@keyframes pieceRight {
  50% {
    right: 80%;
    width: 10%;
  }
}
@media screen and (max-width: 799px) {
  .wrapper .container .one,
  .wrapper .container .two,
  .wrapper .container .three,
  .wrapper .container .circle,
  .wrapper .container .pcenter {
    width: 90%;
    height: 90%;
    top: 5% !important;
    left: 5% !important;
    min-width: 280px;
    min-height: 280px;
  }
}
@media screen and (max-height: 660px) {
  .wrapper .container .one,
  .wrapper .container .two,
  .wrapper .container .three,
  .wrapper .container .circle,
  .wrapper .container .pcenter {
    min-width: 280px;
    min-height: 280px;
    width: 60%;
    height: 60%;
    top: 20% !important;
    left: 20% !important;
  }
}
.wrapper .container .text {
  width: 60%;
  height: 40%;
  min-width: 400px;
  min-height: 500px;
  position: absolute;
  margin: 40px 0;
}
@media screen and (max-width: 799px) {
  .wrapper .container .text {
    min-height: 400px;
    height: 80%;
  }
}
.wrapper .container .text article {
  width: 400px;
  position: absolute;
  bottom: 0;
  z-index: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}
@media screen and (max-width: 799px) {
  .wrapper .container .text article {
    width: 100%;
  }
}
.wrapper .container .text article p {
  color: white;
  font-size: 18px;
  letter-spacing: 0.6px;
  margin-bottom: 40px;
  text-shadow: 6px 6px 10px #32243e;
}
.wrapper .container .pcenter {
  font-size: 200px;
  font-weight: 700;
  letter-spacing: 4px;
  color: white;
  display: flex !important;
  justify-content: center;
  align-items: center;
  position: absolute;
  z-index: 2;
}
@media screen and (max-width: 799px) {
  .wrapper .container .pcenter {
    font-size: 75px;
  }
}

.wrapper .container .pcenter:nth-of-type(2) {
  color: #1a2230;
  z-index: 1;
  animation-delay: 1s;
  filter: blur(10px);
  opacity: 0.8;
}
.wrapper .container .circle {
  position: absolute;
}
.wrapper .container .circle:before {
  content: "";
  position: absolute;
  width: 800px;
  height: 800px;
  background-color: #373951;
  border-radius: 100%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: inset 5px 20px 40px rgba(41, 45, 76, 0.393),
    inset 5px 0px 5px rgba(50, 36, 62, 0.3),
    inset 5px 5px 20px rgba(50, 36, 62, 0.25),
    2px 2px 5px rgba(255, 255, 255, 0.2);
}

@media screen and (max-width: 799px) {
  .wrapper .container .circle:before {
    width: 400px;
    height: 400px;
  }
}
.wrapper .container .one .content:before {
  content: "";
  position: absolute;
  width: 600px;
  height: 600px;
  background-color: #25263630;
  border-radius: 100%;
  box-shadow: inset 5px 20px 40px rgba(53, 61, 98, 0.25),
    inset 5px 0px 5px rgba(36, 38, 62, 0.3),
    inset 5px 5px 20px rgba(50, 36, 62, 0.25),
    2px 2px 5px rgba(255, 255, 255, 0.2);
  animation: circle 0.8s 0.4s cubic-bezier(1, 0.06, 0.25, 1) backwards;
}
@media screen and (max-width: 799px) {
  .wrapper .container .one .content:before {
    width: 300px;
    height: 300px;
  }
}
.wrapper .container .one .content .piece {
  background: linear-gradient(90deg, #6470b9 13.7%, #9754ce 94.65%);
}
.wrapper .container .one .content .piece:nth-child(1) {
  right: 15%;
  top: 18%;
  height: 30px;
  width: 120px;
  animation-delay: 0.5s;
  animation-name: pieceRight;
}
.wrapper .container .one .content .piece:nth-child(2) {
  left: 15%;
  top: 45%;
  width: 150px;
  height: 50px;
  animation-delay: 1s;
  animation-name: pieceLeft;
}
.wrapper .container .one .content .piece:nth-child(3) {
  left: 10%;
  top: 75%;
  height: 20px;
  width: 70px;
  animation-delay: 1.5s;
  animation-name: pieceLeft;
}
.wrapper .container .two .content .piece {
  background: linear-gradient(90deg, #ccb67e 0%, #f66e4f 100%);
}
.wrapper .container .two .content .piece:nth-child(1) {
  left: 0%;
  top: 25%;
  height: 40px;
  width: 120px;
  animation-delay: 2s;
  animation-name: pieceLeft;
}
.wrapper .container .two .content .piece:nth-child(2) {
  right: 15%;
  top: 35%;
  width: 180px;
  height: 50px;
  animation-delay: 2.5s;
  animation-name: pieceRight;
}
.wrapper .container .two .content .piece:nth-child(3) {
  right: 10%;
  top: 80%;
  height: 20px;
  width: 160px;
  animation-delay: 3s;
  animation-name: pieceRight;
}
.wrapper .container .three .content .piece {
  background: #f29090;
}
.wrapper .container .three .content .piece:nth-child(1) {
  left: 25%;
  top: 35%;
  height: 20px;
  width: 80px;
  animation-name: pieceLeft;
  animation-delay: 3.5s;
}
.wrapper .container .three .content .piece:nth-child(2) {
  right: 10%;
  top: 55%;
  width: 140px;
  height: 40px;
  animation-name: pieceRight;
  animation-delay: 4s;
}
.wrapper .container .three .content .piece:nth-child(3) {
  left: 40%;
  top: 68%;
  height: 20px;
  width: 80px;
  animation-name: pieceLeft;
  animation-delay: 4.5s;
}
</style>