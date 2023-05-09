<script setup>

//const emit = defineEmits(["next","prev"]);

defineProps(["inicio", "fin", "maxlength"]); //props como array

</script>

<template> 
<!-- copiamos de bootstrap: -->
<div class="btn-group" role="group" aria-label="Basic example">
  <button
    @click="$emit('prev')"
      type="button"
      class="btn btn-outline-primary"
      :disabled="inicio === 0"
      
     >
     Previus{{ inicio }}</button>
  <button 
    @click="$emit('next')" 
    type="button" 
    class="btn btn-primary"
    :disabled="fin >= maxlength"
    >
    Next{{ fin }}</button>
</div>



</template>