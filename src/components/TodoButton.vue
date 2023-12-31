<script setup>// ------------------------------------SCRIPT------------------------------------------- 

</script>


<template> <!-- -------------------------------------TEMPLATE------------------------------------------- -->
    <button>
        <slot>Create</slot>
    </button>
</template>


<style lang="scss" scoped> //--------------------------------STYLE---------------------------------------
    button {
        padding: 8px 16px;
        border: none;
    }
</style>