<template>
  <div class="form-check form-switch">
    <input class="form-check-input" type="checkbox" :id="id" :checked="isDone" @change="$emit('checkbox-changed')"/>
    <label class="form-check-label" :for="id">{{ label }}</label>
  </div>
</template>

<script>
export default {
  props: {
    label: { required: true, type: String },
    done: { default: false, type: Boolean },
    id: { required: true, type: String }
  },
  data() {
    return {
      isDone: this.done,
    };
  }
};
</script>