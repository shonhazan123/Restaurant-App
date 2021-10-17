<template>
  <header>
    <h1 class="text-center">{{ text }}</h1>
  </header>
</template>

<script>
export default {
  name: "Header",

  props: {
    text: String,
  },
};
</script>
