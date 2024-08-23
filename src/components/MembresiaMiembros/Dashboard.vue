<template>
    <div class="chart-container">
        <h2 class="chart-title">Distribución de membresías por tipo</h2>

        <p class="chart-description">
            Esta gráfica muestra la distribución de los diferentes tipos de membresías disponibles en el sistema.
        </p>

        <div class="doughnut-container">
            <doughnut-chart :data="chartData" :options="chartOptions" />
        </div>
    </div>
</template>
<script>
import { Doughnut } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale)

export default {
    components: {
        DoughnutChart: Doughnut
    },
    data() {
        return {
            labels: [],
            data: [],
            chartData: {
                labels: ['Red', 'Blue'],
                datasets: [
                    {
                        label: 'Membresías por tipo',
                        backgroundColor: ['#FF6384', '#36A2EB'],
                        data: [300, 50]
                    }
                ]
            },
            chartOptions: {
                responsive: true,
                plugins: {
                    legend: {
                        position: 'top',
                    },
                    tooltip: {
                        callbacks: {
                            label: function (tooltipItem) {
                                return tooltipItem.label + ': ' + tooltipItem.raw;
                            }
                        }
                    }
                }
            }
        }
    },
    methods: {
        async getMembresiasCountByType() {
            const url = "http://127.0.0.1:8000/tipo_membresias/"
            const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJOb21icmVfVXN1YXJpbyI6Ikh1Z28iLCJDb3JyZW9fRWxlY3Ryb25pY28iOiJzdHJpbmciLCJDb250cmFzZW5hIjoiMTIzIiwiTnVtZXJvX1RlbGVmb25pY29fTW92aWwiOiJzdHJpbmcifQ.YMBusRBKyHAWmwUSlgTr8c1_qOuU-lf9hp1en5O_CF8"

            const response = await fetch(url, {
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${token}`
                }
            });

            if (!response.ok) {
                throw new Error('Error en la solicitud: ' + response.statusText);
            }

            const apiData = await response.json();
            console.log('Respuesta de la API:', apiData);

            this.labels = Object.keys(apiData)
            this.data = Object.values(apiData)

            this.chartData = {
                labels: [...this.labels],
                datasets: [
                    {
                        label: 'Membresías por tipo',
                        backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56'],
                        data: [...this.data]
                    }
                ]
            };
        }
    },
    created() {
        this.getMembresiasCountByType()
    }
}
</script>
<style scoped>
.chart-container {
    display: flex;
    flex-direction: column;
    max-width: 500px;
    margin: 4vh auto;
    text-align: center;
}

.chart-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 10px;
}

.chart-description {
    font-size: 16px;
    margin-bottom: 20px;
    color: #666;
}

.doughnut-container {
    width: 50vw;
    height: 50vh;
    margin: 0 auto;
}

</style>