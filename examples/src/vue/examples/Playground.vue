<script setup>
import { createSection } from '@formkit/inputs'
import { getCurrentSchemaNode } from '@formkit/vue'

const outer = createSection('outer', () => ({
  $el: 'div',
}))
const innerA = createSection('innerA', () => ({
  $el: 'div',
  children: 'Inner a',
}))
const innerB = createSection('innerB', () => ({
  $el: 'div',
  children: 'Inner b',
}))

function switcher(schemaA, schemaB) {
  console.log('schemaA', schemaA)
  return (extensions) => {
    if (getCurrentSchemaNode().props.attrs.options) {
      return schemaA(extensions)
    }
    return schemaB(extensions)
  }
}

const definition = {
  type: 'input',
  schema: outer(switcher(innerA(), innerB())),
}
</script>

<template>
  <FormKit :type="definition" :options="[]" />
</template>

<style scoped>
/*
vanilla CSS can go here.
Keep styles scoped to avoid multiple files
overwriting each other in the render output.
*/
</style>
