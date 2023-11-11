<template>
  <div class="container">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
  </div>

  <!-- <div class="container"> -->
    <div class="row">
      <!-- Mensaje de bienvenida en el lateral izquierdo -->
      <div class="col-md-3">
        <div class="layout-sidebar">
         <h2 class="mensaje"> ¡Bienvenido al Restaurante "Hucaleros Con Sabor! </h2>
         <h5 class="mensaje2"> Esperamos que disfrutes de nuestra deliciosa comida.</h5>
         <h6 class="mensaje3"> Selecciona los platillos, después da clic en el botón "Enviar pedido"</h6>
         <h6 class="mensaje4"> ¡Buen provecho!</h6>
        </div>
      </div>
    </div>

      <div class="container">
        <div v-if="!pedidoIniciado">
  <!-- Formulario para el nombre del cliente -->
  <div class="row">
    <div class="col-md-6 offset-md-3">
      <div class="form-group">
        <label for="customerName">Nombre del Cliente:</label>
        <input type="text" class="form-control" v-model="customerName" id="customerName" placeholder="Ingrese su nombre">
      </div>
      <button class="btn btn-primary" @click="startOrder">Iniciar Pedido</button>
    </div>
  </div>
  </div>
  
    <!-- MENU DEL RESTAURANTE -->
    <div v-if="!pedidoIniciado">
   <h1 class="my-4">Menú del Restaurante HCS</h1>
   <div class="row">
     <div v-for="(dish, index) in dishes" :key="index" class="col-md-4 mb-4">
       <div class="card">
         <div class="card-body">
           <h5 class="card-title">{{ dish.name }}</h5>
           <p class="card-text">Precio:$ {{ dish.price }}</p>
           <div class="input-group mb-3">
             <input type="number" class="form-control" v-model="dish.quantity" placeholder="Cantidad">
             <div class="input-group-append">
               <button class="btn btn-primary" @click="addToOrder(dish)">Agregar al pedido</button>
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
   </div>
   <div class="my-4">
     <h2>Resumen del pedido</h2>
     <div v-for="(item, index) in order" :key="index" class="mb-2">
       <p>{{ item.name }}: {{ item.quantity }}</p>
     </div>
     
     <button class="btn btn-success" @click="submitOrder">Enviar pedido</button>
     
   </div>
  </div>
 </template>
 
 <!-- <style>
.layout-sidebar {
  background-color: #f8f9fa; /* Color de fondo */
  padding: 20px; /* Espaciado interno */
  border-radius: 8px; /* Bordes redondeados */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); /* Sombra ligera */
}

.mensaje {
  color: #007bff; /* Color del texto principal */
  margin-bottom: 10px; /* Espaciado inferior */
}

.mensaje2 {
  color: #28a745; /* Color del texto secundario */
  margin-bottom: 10px; /* Espaciado inferior */
}

.mensaje3 {
  color: #6c757d; /* Color del texto adicional */
}
</style> -->
 
 <script>
 export default {
  data() {
   return {
     customerName: '',
     dishes: [
       // Aquí puedes agregar los platos disponibles
       { name: 'Enchiladas',  price: 70, quantity: 1 },
       { name: 'Chilaquiles', price: 60, quantity: 1 },
       { name: 'Enfrijoladas',  price: 70, quantity: 1 },
       { name: 'Pechuga empanizada',  price: 90, quantity: 1 },
       { name: 'Flautas',  price: 70, quantity: 1, image:"src/assets/flautas.jpg" },
       { name: 'Milanesa',  price: 90, quantity: 1 },
       { name: 'Pozole',  price: 90, quantity: 1 },
       { name: 'Huevos ranchero',  price: 60, quantity: 1 },
       // Agrega más platos según sea necesario
     ],
     order: [],
     total: 0,
     pedidoIniciado: false,
   };
  },
  methods: {
    startOrder() {
    if (this.customerName.trim() !== '') {
      this.pedidoIniciado = true;
      console.log(`¡Hola, ${this.customerName}! Pedido iniciado.`);
    } else {
      alert('Por favor, ingrese su nombre antes de iniciar el pedido.');
    }
  },
   addToOrder(dish) {
     // Aquí puedes agregar la lógica para agregar un plato al pedido
     const existingDish = this.order.find(item => item.name === dish.name);
    
    if (existingDish) {
      // Si el platillo ya está en el pedido, incrementa la cantidad.
      existingDish.quantity++;
    } else {
      // Si no está en el pedido, agrégalo con cantidad 1.
      this.order.push({ ...dish, quantity: 1 });
      this.calculateTotal();
    }
  },
  calculateTotal() {
    this.total = this.order.reduce((accumulator, item) => {
      return accumulator + item.price * item.quantity;
    }, 0);
  },
   submitOrder() {
     // Aquí puedes agregar la lógica para enviar el pedido
     console.log('Pedido enviado:', this.order);
   },
  },
 };
 
 </script>
 
 