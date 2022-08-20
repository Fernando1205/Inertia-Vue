<script>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import { Head } from '@inertiajs/inertia-vue3';
    import LinkButton from '@/Components/LinkButton.vue';
    import Swal from 'sweetalert2';

    export default {
        components:{
            BreezeAuthenticatedLayout,
            Head,
            LinkButton
        },
        props:{
            blogs: Object,
            flash: Object,
        },
        mounted(){
            if(this.flash.message !== null) {
                Swal.fire(
                'Success!',
                `${this.flash.message}`,
                'success'
                )
            }
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

        <div v-if="$page.props.flash.message"
            class="bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative" role="alert" id="alert">
            <strong class="font-bold">{{ $page.props.flash.message }}</strong>
            <span id="close" class="absolute top-0 bottom-0 right-0 px-4 py-3">
                <svg class="fill-current h-6 w-6 text-green-500" role="button" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><title>Close</title><path d="M14.348 14.849a1.2 1.2 0 0 1-1.697 0L10 11.819l-2.651 3.029a1.2 1.2 0 1 1-1.697-1.697l2.758-3.15-2.759-3.152a1.2 1.2 0 1 1 1.697-1.697L10 8.183l2.651-3.031a1.2 1.2 0 1 1 1.697 1.697l-2.758 3.152 2.758 3.15a1.2 1.2 0 0 1 0 1.698z"/></svg>
            </span>
        </div>

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


