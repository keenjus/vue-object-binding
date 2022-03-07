<template>
  <div>
    {{ modelValue }}
    {{ model }}
    <input type="text" v-model="model.name" />
  </div>
</template>

<script>
import { nextTick, watch, defineComponent, reactive, computed, ref } from 'vue';
import { cloneDeep, isEqual } from 'lodash';

export default defineComponent({
  props: {
    modelValue: Object,
  },
  setup(props, ctx) {
    const model = ref(cloneDeep(props.modelValue));

    watch(
      model,
      (value) => {
        if (isEqual(value, props.modelValue)) return;
        console.log('emit');
        ctx.emit('update:modelValue', cloneDeep(value));
      },
      { deep: true }
    );

    watch(
      () => props.modelValue,
      (value) => {
        console.log('bind');
        model.value = cloneDeep(value);
      },
      { deep: true }
    );

    return {
      model,
    };
  },
});
</script>
