<script>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
    import { Head, Link } from '@inertiajs/inertia-vue3';
    import  Button  from '@/Components/Button.vue';
    import { Inertia } from '@inertiajs/inertia';
    import { reactive } from 'vue';
    import InputError from '@/Components/InputError.vue';

    export default {
        components:{
            BreezeAuthenticatedLayout,
            Head,
            Button,
            Link,
            InputError
        },
        props:{
            errors: Object,
            blog: Object
        },
        setup(props) {
            const form = reactive({
                title: props.blog.title,
                slug: props.blog.slug,
                content: props.blog.content
            })
            function submit() {
                Inertia.put(route('blogs.update', props.blog),form,{
                    preserveScroll:true,
                    onSuccess: () => console.log('Hecho')
                })
            }
            return { form, submit }
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
            <div class="bg-white max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="overflow-hidden">
                    <div class="p-6">

                        <form @submit.prevent="submit">
                            <label class="block mb-4">
                                <span class="block text-sm font-medium text-slate-700">Title</span>
                                <input v-model="form.title" type="text" id="title" name="title" placeholder="Title...."
                                    class="w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm">
                                <InputError :message="errors.title"></InputError>
                            </label>

                             <label class="block mb-4">
                                <span class="block text-sm font-medium text-slate-700">Slug</span>
                                <input v-model="form.slug" type="text" id="slug" name="slug" placeholder="Slug...."
                                    class="w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm">
                                <InputError :message="errors.slug"></InputError>

                            </label>

                             <label class="block mb-4">
                                <span class="block text-sm font-medium text-slate-700">Content</span>
                                <textarea v-model="form.content" type="text" id="content" name="content" placeholder="Content...."
                                    class="w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm">
                                </textarea>
                                <InputError :message="errors.content"></InputError>
                            </label>

                            <Button type="submit">Update</Button>
                        </form>


                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>


