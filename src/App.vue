<template>
    <div id="app">
        <!-- component -->
        <div>
            <div class="relative min-h-screen  grid bg-gray-800 ">
                <div
                    class="flex flex-col sm:flex-row items-center md:items-start sm:justify-center md:justify-start flex-auto min-w-0 ">
                    <div
                        class="relative sm:w-1/2 xl:w-3/5 bg-blue-500 h-full hidden md:flex flex-auto items-center justify-center p-10 overflow-hidden  text-white bg-no-repeat bg-cover relative"
                        style="background-image: url(https://images.unsplash.com/photo-1637102839358-51288f0a30d8?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2070&q=80);">
                        <div class="absolute bg-black  opacity-25 inset-0 z-0"></div>
                        <div class="w-full  lg:max-w-2xl md:max-w-md z-10 items-center text-center ">
                            <div class=" font-bold leading-tight mb-6 mx-auto w-full content-center items-center ">

                            </div>
                        </div>
                    </div>

                    <div
                        class="md:flex md:items-center md:justify-left w-full sm:w-auto md:h-full xl:w-1/2 p-8  md:p-10 lg:p-14 sm:rounded-lg md:rounded-none ">
                        <div class="max-w-xl w-full space-y-12">
                            <div class="lg:text-left text-center">

                                <div class="flex items-center justify-center ">
                                    <div
                                        class="bg-black flex flex-col w-80 border border-gray-900 rounded-lg px-8 py-10">

                                        <form
                                            @submit.prevent="addNewTodo"
                                            class="flex flex-col space-y-8 mt-10">
                                            <label class="font-bold text-lg text-white ">Add your link</label>
                                            <input
                                                type="text"
                                                placeholder="your link"
                                                class="border rounded-lg py-3 px-3 mt-4 bg-black border-indigo-600 placeholder-white-500 text-white"
                                                v-model="full"
                                            >
                                            <button
                                                @click="copyText"
                                                class="border border-indigo-600 bg-black text-white rounded-lg py-3 font-semibold"
                                                v-text=" 'Generate new link' "
                                            />

                                            <a
                                                class="text-center  border border-indigo-600 bg-black text-white rounded-lg py-3 font-semibold"
                                                target="_blank" :href="short">{{ short }}</a>
                                        </form>
                                    </div>
                                </div>

                            </div>

                        </div>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            short: 'your link',
            full: null
        }
    },

    methods: {
        addNewTodo() {
            axios.get('http://127.0.0.1:8000/api/addLink?link=https://' + this.full)
                .then(response => {
                    this.short = response.data.link
                })
        },
        copyText() {
            navigator.clipboard.writeText(this.short)
        }
    },
    mounted() {
        this.addNewTodo();
    }
}
</script>