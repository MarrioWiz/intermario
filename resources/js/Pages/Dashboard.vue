<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import {Bar,Pie} from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, ArcElement } from 'chart.js';
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, ArcElement);
import { ref } from 'vue';
const props = defineProps({
	authors: {type:Object},
	books: {type:Number},
	countries: {type:Object},
});

const aut = ref([]);
const cou = ref([]);
const chartData1 = ref([]);
const charOptions1 = ref([]);
const chartData2 = ref([]);
const charOptions2 = ref([]);
const aut2 = ref([]);
const boo = ref([]);
const colors = ref([]);

const random = () =>{
	return Math.floor(Math.random() *256)
}
//Graphic1
props.countries.map( (row) => (
	cou.value.push(row.country),
	aut.value.push(row.authors.length),
	colors.value.push('rgb('+random()+','+random()+','+random()+')')
))
charOptions1.value = {responsive:true};
chartData1.value = {
	labels:cou.value,
	datasets:[{
		label:'Desarrolladores',data:aut.value,backgroundColor:colors
	}]
}
//Graphic2
props.authors.map( (row) => (
	boo.value.push(row.books.length),
	aut2.value.push(row.last_name+' '+row.name),
	colors.value.push('rgb('+random()+','+random()+','+random()+')')
))
charOptions2.value = {responsive:true};
chartData2.value = {
	labels:aut2.value,
	datasets:[{
		label:'Areas',data:boo.value,backgroundColor:colors
	}]
}

</script>

<template>
	<Head title="Dashboard" />
	
	<AuthenticatedLayout>
		<template #header>
			Dashboard
		</template>
		
		<div class="p-4 bg-white rounded-lg shadow-xs">
			<div class="grid gap-6 mb-8 md:grid-cols-2 xl:grid-cols-4">
              <!-- Card -->
              <div class="flex border items-center p-4 bg-white rounded-lg shadow-xs dark:bg-gray-800">
                <div class="p-3 mr-4 text-orange-500 bg-orange-100 rounded-full dark:text-orange-100 dark:bg-orange-500">
					<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
						<path stroke-linecap="round" stroke-linejoin="round" d="M12 6.042A8.967 8.967 0 0 0 6 3.75c-1.052 0-2.062.18-3 .512v14.25A8.987 8.987 0 0 1 6 18c2.305 0 4.408.867 6 2.292m0-14.25a8.966 8.966 0 0 1 6-2.292c1.052 0 2.062.18 3 .512v14.25A8.987 8.987 0 0 0 18 18a8.967 8.967 0 0 0-6 2.292m0-14.25v14.25" />
					</svg>
                </div>
                <div>
                  <p class="mb-2 text-sm font-medium text-gray-600 dark:text-gray-400">
                    Total Desarrolladores
                  </p>
                  <p class="text-lg font-semibold text-gray-700 dark:text-gray-200">
                    {{ authors.length }}
                  </p>
                </div>
              </div>
              <!-- Card -->
              <div class="flex border items-center p-4 bg-white rounded-lg shadow-xs dark:bg-gray-800">
                <div class="p-3 mr-4 text-green-500 bg-green-100 rounded-full dark:text-green-100 dark:bg-green-500">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M4 4a2 2 0 00-2 2v4a2 2 0 002 2V6h10a2 2 0 00-2-2H4zm2 6a2 2 0 012-2h8a2 2 0 012 2v4a2 2 0 01-2 2H8a2 2 0 01-2-2v-4zm6 4a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd"></path>
                  </svg>
                </div>
                <div>
                  <p class="mb-2 text-sm font-medium text-gray-600 dark:text-gray-400">
                    Total Areas
                  </p>
                  <p class="text-lg font-semibold text-gray-700 dark:text-gray-200">
                    {{ books }}
                  </p>
                </div>
              </div>
              <!-- Card -->
              <div class="flex border items-center p-4 bg-white rounded-lg shadow-xs dark:bg-gray-800">
                <div class="p-3 mr-4 text-blue-500 bg-blue-100 rounded-full dark:text-blue-100 dark:bg-blue-500">
					<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
						<path stroke-linecap="round" stroke-linejoin="round" d="M3 3v1.5M3 21v-6m0 0 2.77-.693a9 9 0 0 1 6.208.682l.108.054a9 9 0 0 0 6.086.71l3.114-.732a48.524 48.524 0 0 1-.005-10.499l-3.11.732a9 9 0 0 1-6.085-.711l-.108-.054a9 9 0 0 0-6.208-.682L3 4.5M3 15V4.5" />
					</svg>
                </div>
                <div>
                  <p class="mb-2 text-sm font-medium text-gray-600 dark:text-gray-400">
                    total countries
                  </p>
                  <p class="text-lg font-semibold text-gray-700 dark:text-gray-200">
                    {{ countries.length }}
                  </p>
                </div>
              </div>
              <!-- Card -->
              <div class="flex border items-center p-4 bg-white rounded-lg shadow-xs dark:bg-gray-800">
                <div class="p-3 mr-4 text-teal-500 bg-teal-100 rounded-full dark:text-teal-100 dark:bg-teal-500">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M18 5v8a2 2 0 01-2 2h-5l-5 4v-4H4a2 2 0 01-2-2V5a2 2 0 012-2h12a2 2 0 012 2zM7 8H5v2h2V8zm2 0h2v2H9V8zm6 0h-2v2h2V8z" clip-rule="evenodd"></path>
                  </svg>
                </div>
                <div>
                  <p class="mb-2 text-sm font-medium text-gray-600 dark:text-gray-400">
                    Pending contacts
                  </p>
                  <p class="text-lg font-semibold text-gray-700 dark:text-gray-200">
                    35
                  </p>
                </div>
              </div>
            </div>
			<div class="grid gap-6 bg-white mb-8 md:grid-cols-2 rounded-lg">
				<div class="min-w-0 p-4 rounded-lg shadow-xs border">
					<span class="text-lg p-4">Desarrolladores by country</span>
					<div class="flex items-center">
						<Bar :data="chartData1" :options="charOptions1"></Bar>
					</div>
				</div>
				<div class="min-w-0 p-4 rounded-lg shadow-xs border">
					<span class="text-lg p-4">Areas by Desarrolladores</span>
					<div class="flex items-center">
						<Pie :data="chartData2" :options="charOptions2" />
					</div>
				</div>
			</div>
		</div>
	</AuthenticatedLayout>
</template>
