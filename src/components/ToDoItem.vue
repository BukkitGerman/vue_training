<template>
  <div class="stack-small" v-if="!isEditing">
    <div class="form-check form-switch">
      <input class="form-check-input" type="checkbox" :id="id" :checked="isDone" @change="$emit('checkbox-changed')"/>
      <label class="form-check-label" :for="id">{{ label }}</label>
    </div>
    <div class="btn-group">
      <button type="button" class="btn-warning"  @click="toggleToItemEditForm" ref="editButton">
        Edit <span class="visually-hidden">{{label}}</span>
      </button>
      <button type="button" class="btn btn-danger" @click="deleteToDo">
        Delete <span class="visually-hidden">{{label}}</span>
      </button>
    </div>
  </div>
  <to-do-item-edit-form v-else :id="id" :label="label"
                        @item-edited="itemEdited"
                        @edit-cancelled="editCancelled">
  </to-do-item-edit-form>
</template>
<script>
import ToDoItemEditForm from "./ToDoItemEditForm";

export default {
  components: {
    ToDoItemEditForm
  },
  props: {
    label: { required: true, type: String },
    done: { default: false, type: Boolean },
    id: { required: true, type: String }
  },
  data() {
    return {
      isEditing: false
    };
  },
  computed: {
    isDone() {
      return this.done;
    }
  },
  methods: {
    deleteToDo() {
      this.$emit('item-deleted');
    },
    toggleToItemEditForm() {
      this.isEditing = true;
    },
    itemEdited(newLabel) {
      this.$emit('item-edited', newLabel);
      this.isEditing = false;
      this.focusOnEditButton();
    },
    editCancelled() {
      this.isEditing = false;
      this.focusOnEditButton();
    },
    focusOnEditButton() {
      this.$nextTick(() => this.$refs.editButton.focus())
    }
  }
};
</script>