<template>
  <div>
    <h1>{{ userName }}</h1>
    <h2>{{ userAge }}</h2>
    <p>{{ injectedAge }}</p>
  </div>
</template>

<script>
import {
  computed,
  inject,
  defineComponent,
  onBeforeMount,
  onMounted,
} from 'vue';

export default defineComponent({
  name: 'UserData',
  props: ['firstName', 'lastName', 'userAge'],
  setup(props, context) {
    const userName = computed(() => {
      return props.firstName + ' ' + props.lastName;
    });
    console.log(context, 'context');

    const injectedAge = inject('userAge');
    // context.emit('save-data', data);

    onBeforeMount(() => {
      console.log('before mount');
    });
    onMounted(() => {
      console.log('mounted');
    });
    return {
      userName,
      injectedAge,
    };
  },
});
</script>

<style lang="scss" scoped></style>
