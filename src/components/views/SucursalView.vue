<template>
    <div class="w-full h-full">
    <div class="w-full h-[70%]">
        <Sucursal></Sucursal>
    </div>
    <div class="w-[80%] ml-[3%]">
        <Footer></Footer>
    </div>
</div>
</template>
<script>
    import Sucursal from '../../components/Sucursal.vue'
    import Footer from '../Footer.vue';
    export default{
        components:
            {
                Sucursal,
                Footer
            }
    }
</script>

