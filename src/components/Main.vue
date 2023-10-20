<template>
    <main>
        <header>
            <nav class="d-flex justify-content-between align-items-center">
                <div class="icon">
                    <i class="fa-solid fa-bars"></i>
                </div>

                <div class="profile d-flex align-items-center">
                    <i class="fa-solid fa-envelope me-3"></i>
                    <div class="image-profile me-3">
                        <img src="../assets/WhatsApp Image 2023-09-09 at 19.22.36.jpeg" alt="">
                    </div>
                    <p class="m-0">Mario Santoro</p>
                </div>
            </nav>
        </header>
        <div class="container-cs h-cs">
            <div class="row justify-content-center h-100">
                <div class="col">
                    <div class="card h-100 border-0 p-3">
                        <div class="card-header bg-transparent text-center">
                            <h6>Monthly Connections</h6>
                        </div>
                        <Line v-if="loaded" :data="lineData" :options="lineOptions" ref="month"
                            style="height: 100% !important;" />
                    </div>
                </div>
            </div>
        </div>
        <div class="container-cs">
            <div class="row justify-content-center h-100">
                <div class="col-6">
                    <div class="card h-100 border-0 p-3">
                        <div class="card-header bg-transparent text-center">
                            <h6>User Age Range</h6>
                        </div>
                        <Bar v-if="loaded" :data="BarData" :options="BarOptions" ref="userAge"
                            style="height: 100% !important;" />
                    </div>
                </div>
                <div class="col-6">
                    <div class="card h-100 border-0 p-3">
                        <div class="card-header bg-transparent text-center">
                            <h6>User Age Range</h6>
                        </div>
                        <Doughnut v-if="loaded" :data="DoughnutData" :options="DoughnutOptions" ref="Doughnut"
                            style="height: 100% !important; width: 100% !important;" />
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>
<script>
import axios from 'axios';
import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Filler,
    ArcElement
} from 'chart.js'
import { Line, Bar, Doughnut } from 'vue-chartjs'
ChartJS.register(CategoryScale, LinearScale, BarElement, Title, Tooltip, Legend, PointElement, LineElement, Filler, ArcElement)
export default {
    data() {
        return {
            loaded: false,
            lineData: {
                labels: [],
                datasets: [
                    {
                        label: 'Monthly',
                        lineTension: 0.4,
                        data: [],
                        fill: true,
                        backgroundColor: 'rgba(160,193,199, 0.2)',
                        borderColor: '#6bb2bf',
                        borderRadius: 100
                    }
                ]
            },
            lineOptions: {
                responsive: true,
                scales: {
                    y: {
                        beginAtZero: true,
                        ticks: {
                            stepSize: 1000
                        }
                    }
                },
            },

            BarData: {
                labels: [],
                datasets: [
                    {
                        label: 'Age',
                        data: [],
                        fill: true,
                        backgroundColor: []
                    }
                ]
            },
            BarOptions: {
                responsive: true,

            },

            DoughnutData: {
                labels: [],
                datasets: [
                    {
                        label: 'System',
                        data: [],
                        fill: true,
                        backgroundColor: []
                    }
                ]
            },
            DoughnutOptions: {
                responsive: false,

            },
        }
    },
    components: { Line, Bar, Doughnut },
    methods: {
        getMonth() {
            axios.get('http://localhost:3000/MonthlyConnections')
                .then((response) => {
                    let newMonth = response.data.map(item => item.connections);
                    let newLabels = response.data.map(item => item.month);
                    this.lineData.labels = newLabels
                    this.lineData.datasets[0].data = newMonth
                })
                .catch((error) => {
                    console.log(error)
                });

            axios.get('http://localhost:3000/UsersAgeRange')
                .then((response) => {
                    let newAge = response.data.map(item => item.connections);
                    let newLabels = response.data.map(item => item.range);
                    this.BarData.labels = newLabels
                    this.BarData.datasets[0].data = newAge
                    let labels = ['#3D95CD', '#8E5EA3', '#5ABB9F', '#E8C3B8', '#C45850'];
                    for (let i = 0; i < labels.length; i++) {
                        this.BarData.datasets[0].backgroundColor.push(labels[i]);
                    }
                })
                .catch((error) => {
                    console.log(error)
                });

            axios.get('http://localhost:3000/Devices')
                .then((response) => {
                    let newSystem = response.data.map(item => item.connections);
                    let newLabels = response.data.map(item => item.os);
                    this.DoughnutData.labels = newLabels
                    this.DoughnutData.datasets[0].data = newSystem
                    let labels = ['#3D95CD', '#8E5EA3', '#5ABB9F', '#E8C3B8', '#C45850'];
                    for (let i = 0; i < labels.length; i++) {
                        this.DoughnutData.datasets[0].backgroundColor.push(labels[i]);
                    }
                    this.loaded = true
                })
                .catch((error) => {
                    console.log(error)
                })
        }
    },
    mounted() {
        this.getMonth()
    }
}
</script>
<style lang="scss" scoped>
main {
    width: calc(100% - 12%);
    height: 100vh;
    background-color: #F7F7F7;
    overflow-y: auto;

    nav {
        padding: 1rem;
        background-color: #EDEDED;

        div.image-profile {
            width: 40px;
            height: 40px;
        }
    }

    div.container-cs {
        width: calc(100%);
        padding: 0 40px;
        margin-top: 2rem;
    }

    .h-cs {
        height: 280px;
    }
}
</style>