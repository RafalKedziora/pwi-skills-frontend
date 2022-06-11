<template>
    <ProjectList></ProjectList>
</template>

<script>
import { defineComponent } from 'vue';
import ProjectList  from '@/components/ProjectList';

export default defineComponent({
  name: 'HomeView',

  components: {
    ProjectList
  },
});
</script>
