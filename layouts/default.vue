<template>
  <div>
    <div>
      <Nuxt />
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  head() {
    return {
      htmlAttrs: {
        lang: this.$i18n.locale,
        dir: "ltr",
      },
    };
  },
};
</script>

<style></style>
