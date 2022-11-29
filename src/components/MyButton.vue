<template>
    <button
      @click="setTimeFive"
      >
      </button>
</template>

<script>

export default({
    props:{
        sign:{
            type: String,
            required: true,
            default:'',
        }

    }
})
</script>
