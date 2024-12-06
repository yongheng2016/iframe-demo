<template>
  <div @mouseover="preloadIframe('your-page-1.html')" @click="onClick">
    <div
      class="absolute-top"
      style="right: 0"
      @mouseover="mouseoverHandler"
      @mouseout="mouseoutHandler"
    >
      {{ confirm ? "show" : "hide" }}
    </div>
    <slot></slot>
  </div>
  <q-page class="flex flex-center">
    <div
      class="container bg-white"
      v-show="confirm"
      :style="{ marginLeft: left, marginTop: `${top}` }"
    >
      <div
        class="relative-position bg-gold wrapper"
        style="width: 800px; height: 600px"
      >
        <div class="text-right">
          <q-btn flat icon="close" @click="onClick" />
        </div>
        <iframe
          style="width: 800px; height: 600px; background-color: #fff"
          frameborder="0"
          :src="`${url}?type=${randomStr}`"
          v-if="url"
        ></iframe>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
const props = defineProps({
  path: {
    type: String,
    required: true,
  },
  left: String,
  top: String,
});
const confirm = ref(false);
const iframeRef = ref();
const loading = ref(false);
const randomStr = ref("");
const url = ref("");
import { onMounted } from "vue";
import axios from "axios";
const htmlContent = ref("");
onMounted(() => {});
const onload = () => {
  console.log("onload");
};

function loadIframe() {
  const iframe = document.createElement("iframe");
  iframe.src = "https://vault.yangyongheng.olares.cn"; // 替换为你想要加载的 URL
  iframe.id = "myIframe";
  document.getElementById("iframeContainer").appendChild(iframe);
}

requestIdleCallback(() => {
  url.value = props.path;
});

// if ("requestIdleCallback" in window) {
//   requestIdleCallback(loadIframe);
// } else {
//   // 如果不支持 requestIdleCallback，直接加载
// }
const handleIframeLoad = () => {
  // const iframeDocument = iframeRef.value.contentDocument;
  // console.log("aaaa", iframeRef.value.contentDocument);
  return;

  const iframe = document.getElementById("myIframe");
  const doc = iframe.contentDocument || iframe.contentWindow.document;
  doc.open();
  doc.write(htmlContent.value);
  doc.close();
};

function preloadIframe(src) {
  console.log("aaaaaa");
  if (!url.value) {
    url.value = props.path;
  } else {
  }
}

requestIdleCallback(() => {
  console.log("testaaaa");
  url.value = props.path;
});

const onClick = () => {
  // loading.value = true;
  confirm.value = !confirm.value;
  if (!confirm.value) {
    // randomStr.value = Math.random();
    requestIdleCallback(() => {
      // randomStr.value = Math.random();
    });
  }
};

function iconMouseMoveHandler(event) {
  const rect = event.target.getBoundingClientRect();
  console.log("iconMouseMoveHandler", event.clientX, rect.left);

  if (
    event.clientX >= rect.left &&
    event.clientX <= rect.right &&
    event.clientY >= rect.top &&
    event.clientY <= rect.bottom
  ) {
    // 如果鼠标进入图标区域，设置预加载

    clearTimeout(hoverTimeout);
    hoverTimeout = setTimeout(() => {
      preload(icon.dataset.content);
    }, 500); // 设置悬停时间阈值
  } else {
    clearTimeout(hoverTimeout);
  }
}
</script>
<style lang="scss" scoped>
.container {
  position: absolute;
  top: 50%;
  left: 0px;
  transform: translate(-60%, -50%);
  display: flex;
  align-items: center;
  justify-content: center;
  animation: height 1s ease-in;
  background: #fff;
}
.wrapper {
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.2), 0 2px 2px rgba(0, 0, 0, 0.14),
    0 3px 1px -2px rgba(0, 0, 0, 0.12);
  overflow: hidden;
}
.show {
  height: 100%;
}
</style>
