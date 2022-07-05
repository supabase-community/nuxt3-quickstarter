<script setup>
const client = useSupabaseClient()

const { data: tasks } = await useAsyncData('random', () => {
  return client.from('random').select()
})

const counter = useState('counter', () => 1)



</script>
<template>
  <div>
    <h1>some</h1>
    <button @click="counter++">{{ counter }}</button>
    <pre>{{ tasks }}</pre>
  </div>
</template>
