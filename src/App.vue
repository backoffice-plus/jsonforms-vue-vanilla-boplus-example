<template>

  <header>

    <h1>JSON Forms Vue Vanilla Renderer by backoffice.plus</h1>

    <a href="https://github.com/backoffice-plus/jsonforms-vue-vanilla-boplus" target="_blank">
        <img src="https://github.com/fluidicon.png" alt="GitHub Logo">
        GitHub Repository
      </a>

  </header>


  <section>

    <article class="withoutBo">
      <h2>Jsonforms Vue Vanilla (v3.2.1)</h2>
      <JsonForms
          :schema="jf.schema"
          :uischema="jf.uischema"
          :data="jf.data ?? {}"
          :renderers="renderers"
          :i18n="i18n"
          key="vanilla"
      />
    </article>

    <article class="withBo">
      <h2>Bo+ Renderers</h2>
      <JsonForms
          :schema="jf.schema"
          :uischema="jf.uischema"
          :data="jf.data ?? {}"
          :renderers="renderersBop"
          :i18n="i18n"
          key="bo+"
      />
    </article>

  </section>

  <section class="content">
    <div>
      <details>
        <summary>Schema & Ui Schema</summary>
        <textarea readonly disabled>{{jf}}</textarea>
      </details>
    </div>
  </section>

</template>


<style scoped>
header {
  text-align: center;
  padding:2rem;
}

header > a {
  display: flex;
  align-items: center;
  justify-content: center;
}

header > a > img {
  height:36px
}

section {
  display: grid;
  grid-template-columns: minmax(20px,1fr) minmax(300px,40%) minmax(300px,40%) minmax(20px,1fr);
  grid-template-areas:
    ". form1 form2 .";
  grid-gap: 2rem;
}
section article {
  background-color: #f6f7fa;
  border:1px solid #eee;
  padding:2rem;
  padding-top:0;
}

section article.withBo {
  grid-area: form1;
}
section article.withoutBo {
  grid-area: form2;
}

section.content {
  grid-template-areas: ". content content ."
}
section.content > * {
  grid-area: content;
}

details textarea {
  width: 100%;
  aspect-ratio: 5/2;
  font-family: monospace;
}

</style>


<style>
.horizontal-layout {
  display: flex;
  flex-direction: row;
}
fieldset.group {
  min-height:150px;
  margin-bottom:20px;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
button.array-list-item-delete:empty:after {
  content:" 🗙 "
}
input[data-type=password] + button:after {
  content:" <-> "
}
</style>


<script setup lang="ts">
import type {JsonFormsRendererRegistryEntry} from "@jsonforms/core";
import {JsonForms, type MaybeReadonly} from "@jsonforms/vue";
import {vanillaRenderers} from "@jsonforms/vue-vanilla";
import boplusVueVanillaRenderers from "@backoffice-plus/jsonforms-vue-vanilla";
import jf from "./default.forms.json";
import "@backoffice-plus/jsonforms-vue-vanilla/lib/bundle.css"

const renderers:MaybeReadonly<JsonFormsRendererRegistryEntry[]> = Object.freeze([
  ...vanillaRenderers,
]);
const renderersBop:MaybeReadonly<JsonFormsRendererRegistryEntry[]> = Object.freeze([
  ...vanillaRenderers,
  ...boplusVueVanillaRenderers,
]);

const catalogueDe:Record<string, string> = {
  next:"weiter",
  back:"zurück",
};
const i18n = {
  locale: "de",
  translate: (key:string, defaultMessage?:string) => catalogueDe[key] ?? defaultMessage,
}
</script>


