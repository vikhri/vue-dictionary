<template>
  <div class="container">
    <div class="loader">
      <div class="loader--dot"></div>
      <div class="loader--dot"></div>
      <div class="loader--dot"></div>
    </div>
<!--    <div class="loader&#45;&#45;text">Loading</div>-->
  </div>

</template>

<script>

</script>

<style scoped>


.container {
  position: relative;
  height: 100%;
  width: 100%;
  padding-top: 30px;
  color: black;
}

.loader {
  display: flex;
  align-items: center;
  height: 50px;
  width: 200px;
  margin: auto;
}

.loader--dot {
  animation-name: loader;
  animation-timing-function: ease-in-out;
  animation-duration: 3s;
  animation-iteration-count: infinite;
  height: 10px;
  width: 10px;
  border-radius: 50%;
  background-color: white;
  position: absolute;
}

.loader--dot:first-child {
  background-color: #489DFF;
  opacity: 1;
  animation-delay: 0.5s;
}
.loader--dot:nth-child(2) {
  background-color: #489DFF;
  opacity: 0.8;
  animation-delay: 0.3s;
}
.loader--dot:nth-child(3) {
  background-color: #489DFF;
  opacity: 0.5;
  animation-delay: 0.2s;
}
.loader--text {
  width: 4rem;
  margin: auto;
  color: #489DFF;
}
.loader--text:after {
  position: absolute;
  content: "";
  animation: loading-text 3s infinite;
}


@keyframes loader {
15% {
  transform: translateX(0);
}
45% {
  transform: translateX(190px);
}
65% {
  transform: translateX(190px);
}

95% {
  transform: translateX(0);
}
}


@keyframes loading-text {
  0% { content: "";}
  25% {content: ".";}
  50% {content: "..";}
  75% {content: "...";}
}







</style>