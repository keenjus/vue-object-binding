<template>
  <div>
    {{ user }}
    <input type="text" v-model="user.name" />
    <UserEditor :modelValue="user" @update:modelValue="handleUpdate" />
  </div>
</template>

<script>
import { ref } from 'vue';
import UserEditor from './UserEditor.vue';

export default {
  components: {
    UserEditor,
  },
  props: {
    msg: String,
  },
  setup() {
    const user = ref({ name: 'peeter' });

    const handleUpdate = (value) => {
      value.name += 'xxx';
      user.value = value;
    };

    return {
      user,
      handleUpdate,
    };
  },
};
</script>
