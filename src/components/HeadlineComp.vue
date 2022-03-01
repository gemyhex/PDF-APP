<template>
  <div class="accordion" id="accordionExample">
    <div class="accordion-item">
      <h2 class="accordion-header" :id="'heading' + id">
        <button
          class="accordion-button collapsed"
          type="button"
          data-bs-toggle="collapse"
          :data-bs-target="'#collapse' + id"
          aria-expanded="true"
          :aria-controls="'collapse' + id"
        >
          {{ title }}
        </button>
      </h2>
      <div
        :id="'collapse' + id"
        class="accordion-collapse collapse"
        :aria-labelledby="'heading' + id"
        data-bs-parent="#accordionExample"
      >
        <div class="accordion-body">
          {{ content }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["title", "content", "id"],
  data() {
    return {
      cur: 0,
    };
  },
};
</script>

<style scoped>
.drag-zone {
  width: 500px;
  max-width: 500px;
  max-height: 100vh;
  display: flex;
}
</style>
