<template>
  <div>
    <h1>{{ page.title }}</h1>
    <p>{{ page.description }}</p>
    <nuxt-content :document="page" />
  </div>
</template>

<script>
import Vue from "vue";
import MyComponent from "~/components/MyComponent";

Vue.component("MyComponent", MyComponent);

export default {
  async asyncData({ $content, params, error }) {
    const slug = params.slug || "index";
    const page = await $content(slug)
      .fetch()
      .catch((err) => {
        error({ statusCode: 404, message: "Page not found" });
      });

    return {
      page,
    };
  },
};
</script>
