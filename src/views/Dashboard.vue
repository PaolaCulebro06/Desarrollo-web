<template>
  <div class="grid">
    <div class="col-12 md:12">
      <div class="card p-fluid">
        <div class="card-body">
          <h4 class="card-title">Lista de Empleados</h4>
          <div class="table-responsive">
            <table class="table table-bordered table-striped">
              <thead>
                <tr>
                  <th>ID</th>
                  <th>Nombre</th>
                  <th>Salario</th>
                  <th>Foto</th>
                  <th>Acciones</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="empleado in empleados" :key="empleado.id">
                  <td>{{ empleado.id }}</td>
                  <td>{{ empleado.employee_name }}</td>
                  <td>{{ formatCurrency(empleado.employee_salary) }}</td>
                  <td>{{ empleado.profile_image }}</td>
                  <td>
                    <button class="btn btn-success btn-sm" @click="editarEmpleado(empleado)">Editar</button>
                    <button class="btn btn-danger btn-sm" @click="eliminarEmpleado(empleado)">Eliminar</button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        <div class="card-footer">
          <button class="btn btn-primary" @click="agregarEmpleado">Agregar Empleado</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  export default{
    data(){
      return{ empleados: null,
      tituloTabla: "Lista de Empleados",
      textoBotonAgregar: "Agregar Empleado",
      paginado: true,
      inicioPagina: 0,
      tamanoPagina: 10,
      ordenAscendiente: true,
      columnaOrden: null,
      columnas:[
        {titulo:"ID", dato:"id", key:"id"},
        {titulo:"Nombre", dato:"employee_name", key:"employee_name"},
        {titulo:"Salario", dato:"employee_salary", key:"employee_salary"},
        {titulo:"Foto", dato:"profile_image", key:"profile_image"}
      ],
      botones:[
        {texto:"Editar", clase:"btn-success btn-sm", accion:"editarEmpleado"},
        {texto:"Eliminar", clase:"btn-danger btn-sm", accion:"eliminarEmpleado"}
      ],
    };
    },
    mounted(){ 
      this.getEmpleados();
    },
    methods:{
      getEmpleados(){
        axios.get('https://dummy.restapiexample.com/api/v1/employees').then(
          response =>(
            this.empleados = response.data.data
          )
        );
      },
      formatCurrency(value) {
        return "$" + value.toFixed(2);
      },
    
    formatCurrency(value) {
        return "$" + value.toFixed(2);
      },
      ejecutarAccion(accion, empleado) {
        // Lógica para ejecutar acciones como editar o eliminar
        if (accion === "editarEmpleado") {
          this.editarEmpleado(empleado);
        } else if (accion === "eliminarEmpleado") {
          this.eliminarEmpleado(empleado);
        }
        // Agrega más lógica según sea necesario
      },
      
    },
    ordenarPorColumna(columna) {
        if (this.columnaOrden === columna) {
          this.ordenAscendente = !this.ordenAscendente;
        } else {
          this.columnaOrden = columna;
          this.ordenAscendente = true;
        }
      }
  }
</script>



<style scoped>
.table {
  width: 100%;
  margin-bottom: 1rem;
  color: #212529;
  border-collapse: collapse;
}

.table th,
.table td {
  padding: 0.75rem;
  vertical-align: top;
  border-top: 1px solid #dee2e6;
}

.table thead th {
  vertical-align: bottom;
  border-bottom: 2px solid #dee2e6;
}

.table tbody + tbody {
  border-top: 2px solid #dee2e6;
}

.table-sm th,
.table-sm td {
  padding: 0.3rem;
}

.btn {
  display: inline-block;
  font-weight: 400;
  color: #212529;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  background-color: transparent;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
    border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.btn-primary {
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}

.btn-success {
  color: #fff;
  background-color: #28a745;
  border-color: #28a745;
}

.btn-danger {
  color: #fff;
  background-color: #dc3545;
  border-color: #dc3545;
}

.btn-sm {
  padding: 0.25rem 0.5rem;
  font-size: 0.875rem;
  line-height: 1.5;
  border-radius: 0.2rem;
}
</style>
