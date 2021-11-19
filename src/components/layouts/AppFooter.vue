<template>
  <div class="container-fluid bg-dark text-white text-start app-footer py-4">
    <div class="container h-100">
      <div class="d-flex align-items-center">
        <span>author: anakincore</span>
      </div>
      <div class="d-flex align-items-center">
        github:
        <a :href="githubLink" target="_blank" class="text-white ms-1">
          {{ githubLink }}
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppFooter',
  data() {
    return {
      githubLink: 'https://github.com/anakincoresdev',
    };
  },
}
</script>

<style lang="scss" scoped>
  .app-footer {
    height: 100px;
  }
</style>
