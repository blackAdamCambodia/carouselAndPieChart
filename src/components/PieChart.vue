<script setup>
import { onBeforeMount, onMounted, onBeforeUnmount, ref } from 'vue';

let pieChart = null


// chart data
const data = {
    labels: [
        'Red',
        'Green',
        'Yellow'
    ],
    datasets: [{
        data: [30, 40, 30],
        backgroundColor: [
            'red',
            'green',
            'yellow'
        ],
        hoverOffset: 4
    }]
};

// Pie chart configuration
const pieConfig = {
    type: 'pie',
    data: data,
    options: {
        responsive: true
    }
};



onBeforeMount(() => {
    console.log("Before Mounted")
})

onMounted(() => {
    // Get a reference to the canvas element
    const pieCtx = document.getElementById('myPieChart').getContext('2d');


    // Create the pie chart
    pieChart = new Chart(pieCtx, pieConfig);

})

onBeforeUnmount(() => {
    data.labes = []
    data.datasets = []
})

const colorName = ref('')
const colorParcent = ref('')

function updateChart() {
    data.labels.push(colorName.value)
    data.datasets[0].data.push(colorParcent.value)
    data.datasets[0].backgroundColor.push(colorName.value.toLowerCase())

    pieChart.update()
}

</script>

<template>
    <div>
        <div class="w-1/2 mx-auto">
            <h1 class="text-2xl text-gray-900 text-center">Pie Chart</h1>
            <canvas id="myPieChart"></canvas>
            <form class="mt-6 mx-auto">
                <div class="grid gap-6 mb-6  ">
                    <div>
                        <input v-model="colorName" type="text" id="color-name"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            required placeholder="Color Name">
                    </div>
                    <div>
                        <input v-model="colorParcent" type="number" id="color-parcent"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            required placeholder="Parcent">
                    </div>


                </div>
            </form>
        </div>

    </div>
</template>

<style scoped></style>
