<!-- src/views/Dashboard.vue -->
<template>
    <div class="dashboard">
      <h1>Dashboard</h1>
      <div class="charts-container">
        <div class="chart-item">
          <Grafica1 />
        </div>
        <div class="chart-item">
          <Grafica2 />
        </div>
        <div class="chart-item">
          <Grafica3 />
        </div>
        <div class="chart-item">
          <Grafica4 />
        </div>
        <div class="chart-item">
          <AreasChart />
        </div>
        <div class="chart-item">
          <HorariosChart />
        </div>
        <div class="chart-item">
          <EmpleadosChart />
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Grafica1 from '@/components/Grafica1.vue';
  import Grafica2 from '@/components/Grafica2.vue';
  import Grafica3 from '@/components/Grafica3.vue';
  import Grafica4 from '@/components/Grafica4.vue';
  import AreasChart from '@/components/AreasChart.vue';
  import HorariosChart from '@/components/HorariosChart.vue';
  import EmpleadosChart from '@/components/EmpleadosChart.vue';
  
  export default {
    components: {
      Grafica1,
      Grafica2,
      Grafica3,
      Grafica4,
      AreasChart,
      HorariosChart,
      EmpleadosChart
    }
  };
  </script>
  
  <style scoped>
  .dashboard {
    padding: 20px;
  }
  
  .charts-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px; /* Espacio entre los gráficos */
  }
  
  .chart-item {
    flex: 1;
    min-width: 300px; /* Ancho mínimo del gráfico */
    max-width: 500px; /* Ancho máximo del gráfico */
    box-sizing: border-box;
    padding: 10px;
  }
  
  .chart-item canvas {
    width: 100% !important; /* Hace que el canvas se ajuste al contenedor */
    height: 300px !important; /* Ajusta la altura del gráfico */
  }
  </style>
  