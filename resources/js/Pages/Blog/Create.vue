<script>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import { Head, Link } from '@inertiajs/inertia-vue3';
    import  Button  from '@/Components/Button.vue';

    export default {
        components:{
            BreezeAuthenticatedLayout,
            Head,
            Button,
            Link
        },
        props:{
            blogs: Object
        }
    }

</script>
<template>
    <Head title="Blogs"></Head>

    <BreezeAuthenticatedLayout>
       <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Blogs
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="overflow-hidden">
                    <div class="p-6">

                        <section class="border-solid border-2 border-gray-100 rounded-lg shadow-lg">
                            <h1>Hola crear</h1>
                        </section>

                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>


