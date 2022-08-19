<script>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import { Head } from '@inertiajs/inertia-vue3';
    import LinkButton from '@/Components/LinkButton.vue';

    export default {
        components:{
            BreezeAuthenticatedLayout,
            Head,
            LinkButton
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

                        <section class="grid grid-cols-2 gap-4 mb-2">
                            <div>
                                <p>A list of all blogs in your account.</p>
                            </div>
                            <div>
                                <LinkButton :href="route('blogs.create')" class="float-right">Add Blog</LinkButton>
                            </div>
                        </section>
                        <section class="border-solid border-2 border-gray-100 rounded-lg shadow-lg">
                            <table class="auto w-full">
                                <thead class="text-left border-solid border-b-2 border-gray-100">
                                    <tr>
                                        <th class="p-3 bg-white rounded-tl-lg">Title</th>
                                        <th class="p-3 bg-white">Slug</th>
                                        <th class="p-3 bg-white rounded-tr-lg">Content</th>
                                        <th class="p-3 bg-white rounded-tr-lg"></th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="blog in blogs" :key="blog.id" class="border-solid border-b-2 border-gray-100">
                                        <td class="p-3 bg-white">{{ blog.title }}</td>
                                        <td class="p-3 bg-white">{{ blog.slug }}</td>
                                        <td class="p-3 bg-white">{{ blog.content }}</td>
                                        <td class="p-3 bg-white">
                                            <a href="#">Edit</a>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </section>

                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>


