<script setup> 
//defineProps(['title','id','body'])

// const props= defineProps(['title','id','body','colorText'])
// console.log(props.title)
// console.log(props.id)

defineProps({ //props como objeto
    title: String,
    id: Number,
    body:{
        type: String,
        default: 'Sin descripcion',
    },
});

const emit = defineEmits(["cambiarFavoritoNombre"]);

//emit('cambiarFavoritoNombre', title)

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 
                class="card-title"
                
            >{{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button 
            @click="$emit('cambiarFavoritoNombre', title)" 
            class = "btn btn-outline-primary"
            >
            Favorito
        </button>
        </div>
        <!-- :class="`text-${colorText}`" -->
    </div>
</template>