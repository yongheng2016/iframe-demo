<template>
  <q-page class="flex flex-center">
    <DemoPageVue
      v-for="(item, index) in list"
      :path="item"
      :key="item"
      :left="`${index * 40}px`"
      :top="`${index * 40}px`"
    >
      <q-btn
        color="primary"
        :label="item.split('https://')[1].split('.yangyongheng.olares.cn')[0]"
        class="absolute-top"
        no-caps
        style="z-index: 9999; width: 120px; margin-left: 300px"
        :style="{ left: `${index * 120 + 40}px` }"
      />
    </DemoPageVue>

    <DemoPageVue
      v-for="(item, index) in list2"
      :path="item"
      :key="item"
      :left="`${(index + 2) * 40}px`"
      :top="`${(index + 2) * 12}px`"
    >
      <q-btn
        color="primary"
        :label="item.split('https://')[1].split('.yangyongheng.olares.cn')[0]"
        class="absolute-top"
        no-caps
        style="z-index: 9999; width: 120px; margin-left: 300px"
        :style="{ left: `${(index + 2) * 120 + 40}px` }"
      />
    </DemoPageVue>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
import DemoPageVue from "./DemoPage.vue";
const confirm = ref(false);
const iframeRef = ref();
const loading = ref(false);
const randomStr = ref("");

const list = [
  "https://files.yangyongheng.olares.cn",
  // "https://market.yangyongheng.olares.cn",
  // "https://settings.yangyongheng.olares.cn",
  // "https://profile.yangyongheng.olares.cn",
  // "https://dashboard.yangyongheng.olares.cn",
  // "https://control-hub.yangyongheng.olares.cn",
  // "https://wise.yangyongheng.olares.cn",
  // "https://vault.yangyongheng.olares.cn",
];

const list2 = [
  // "https://profile.yangyongheng.olares.cn",
  // "https://dashboard.yangyongheng.olares.cn",
  // "https://control-hub.yangyongheng.olares.cn",
  // "https://wise.yangyongheng.olares.cn",
  // "https://vault.yangyongheng.olares.cn",
];
</script>
<style lang="scss" scoped></style>
