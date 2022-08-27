<script>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import { Head } from '@inertiajs/inertia-vue3';
    import LinkButton from '@/Components/LinkButton.vue';
    import Swal from 'sweetalert2';
    import { Inertia } from '@inertiajs/inertia';

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
                );
            }
        },
        methods: {
            deleteBlog: function(blog) {
                Swal.fire({
                    title: `Are you sure to delete ${blog.title}?`,
                    text: "You won't be able to revert this!",
                    icon: 'warning',
                    showCancelButton: true,
                    confirmButtonColor: '#3085d6',
                    cancelButtonColor: '#d33',
                    confirmButtonText: 'Yes, delete it!'
                })
                .then((result) => {
                    if (result.isConfirmed) {
                        Inertia.delete(route('blogs.destroy',blog), {
                            onSuccess:() => {
                                Swal.fire(
                                    'Deleted!',
                                    `${this.flash.message}`,
                                    'success'
                                )
                            }
                        });

                    }
                });
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
                                <LinkButton :href="route('blogs.create')" class="float-right">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                        <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
                                    </svg>
                                    Add Blog
                                </LinkButton>
                            </div>
                        </section>
                        <section class="border-solid border-2 border-gray-100 rounded-lg shadow-lg">
                            <table class="auto w-full">
                                <thead class="text-left border-solid border-b-2 border-gray-100">
                                    <tr>
                                        <th class="p-3 bg-white rounded-tl-lg">Title</th>
                                        <th class="p-3 bg-white">Slug</th>
                                        <th class="p-3 bg-white rounded-tr-lg">Content</th>
                                        <th class="p-3 bg-white rounded-tr-lg w-2/12 text-center">Acciones</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="blog in blogs" :key="blog.id" class="border-solid border-b-2 border-gray-100">
                                        <td class="p-3 bg-white">{{ blog.title }}</td>
                                        <td class="p-3 bg-white">{{ blog.slug }}</td>
                                        <td class="p-3 bg-white">{{ blog.content }}</td>
                                        <td class="p-3 bg-white text-center">
                                            <LinkButton :href="route('blogs.show', blog)" class="mr-1 bg-green-700 px-2 py-1">
                                                <svg xmlns="http://www.w3.org/2000/svg"
                                                    fill="none" viewBox="0 0 24 24"
                                                    stroke-width="1.5" stroke="currentColor"
                                                    class="w-5 h-5">
                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z" />
                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                                </svg>

                                            </LinkButton>
                                            <LinkButton :href="route('blogs.edit', blog)" class="mr-1 bg-blue-700 px-2 py-1">
                                                <svg xmlns="http://www.w3.org/2000/svg"
                                                    fill="none" viewBox="0 0 24 24"
                                                    stroke-width="1.5" stroke="currentColor"
                                                    class="w-5 h-5">
                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10" />
                                                </svg>
                                            </LinkButton>
                                            <LinkButton @click="deleteBlog(blog)" class="bg-red-700 px-2 py-1">
                                                <svg xmlns="http://www.w3.org/2000/svg"
                                                    fill="none" viewBox="0 0 24 24"
                                                    stroke-width="1.5" stroke="currentColor"
                                                    class="w-5 h-5">
                                                    <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                                                </svg>
                                            </LinkButton>
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


