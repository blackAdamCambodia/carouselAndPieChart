<script setup>
import { ref, reactive, onMounted, onBeforeUnmount, nextTick } from 'vue'

const items = ref([
    {
        title: 'A group of people standing on the top of the sandy beach',
        url: 'https://images.unsplash.com/photo-1691603136732-952a3c6e0ecd?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80'
    },
    {
        title: 'what a wonderful moment ',
        url: 'https://images.unsplash.com/photo-1609908119408-c5f407e10d06?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1548&q=80'
    },
    {
        title: 'A busy city but i feel alone ',
        url: 'https://images.unsplash.com/photo-1570053633105-c87cb16b4976?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1548&q=80'
    },
    {
        title: 'A small village on a cliff surrounded by tree',
        url: 'https://images.unsplash.com/photo-1690824183076-4cedd2986e20?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1740&q=80'
    },
])

let carousel = null

onMounted(() => {
    carousel = new Flickity('#carousel', {});
})

onBeforeUnmount(() => {
    carousel.destroy()
})

let newItem = reactive({
    title: '',
    url: ''
})

function updateCarousel() {
    items.value.push(newItem)
    console.log(items)
    carousel.destroy()

    nextTick(() => {
        carousel = new Flickity('#carousel', {});
    })
}

</script>
<template>
    <div>
        <div class="mx-auto items" id="carousel">
            <div class="item" :style="`background-image:url(${item.url})`" v-for="(item, index) in items" :key="index">
                <p class="pl-12 pr-12 pt-80 text-white font-bold ">{{ item.title }}</p>
            </div>
        </div>
        <form>
            <div class="grid gap-6 mb-6 md:grid-cols-3">
                <div>
                    <input v-model="newItem.url" type="text" id="color-name"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                        required placeholder="Image URL">
                </div>
                <div>
                    <input v-model="newItem.title" type="text" id="color-name"
                        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                        required placeholder="Title">
                </div>

                <div>
                    <button @click.prevent="updateCarousel()" type="submit"
                        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Add
                        to Carousel</button>
                </div>
            </div>
        </form>
    </div>
</template>

<style scoped>
.items {
    width: 1000px;
    height: 500px;
}

.item {
    width: 1000px;
    height: 400px;
    background-color: gray;
    background-size: cover;
}
</style>
