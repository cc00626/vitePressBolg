<!--Layout.vue-->
<template>
  <Layout>
    <template #doc-footer-before> </template>
    <template #doc-after>
      <div style="margin-top: 24px">
        <Giscus :key="page.filePath" repo="cc00626/vitePressBolg" repo-id="R_kgDOO-SQ8Q" category="General"
          category-id="DIC_kwDOO-SQ8c4CrsuS" mapping="pathname" strict="0" reactions-enabled="1" emit-metadata="1"
          input-position="top" lang="zh-CN" loading="lazy" crossorigin="anonymous" :theme="isDark ? 'dark' : 'light'" />
      </div>
    </template>
  </Layout>
</template>

<script lang="ts" setup>
import Giscus from "@giscus/vue";
import DefaultTheme from "vitepress/theme";
import { watch } from "vue";
import { inBrowser, useData } from "vitepress";

const { isDark, page } = useData();

const { Layout } = DefaultTheme;

watch(isDark, (dark) => {
  if (!inBrowser) return;

  const iframe = document
    .querySelector("giscus-widget")
    ?.shadowRoot?.querySelector("iframe");

  iframe?.contentWindow?.postMessage(
    { giscus: { setConfig: { theme: dark ? "dark" : "light" } } },
    "https://giscus.app"
  );
});
</script>