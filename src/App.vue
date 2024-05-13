<template>
  <div id="app" class="py-3">
    <header>
      <h1 class="text-center font-monospace text-decoration-underline">Nuevos Lanzamientos.</h1>
    </header>

    <main class="container">
      <section class="row justify-content-center g-3">
        <div
          class="col-12 col-md-6 col-lg-4"
          v-for="producto in productos"
          :key="producto.id"
        >
          <div class="card">
            <img
              :src="producto.pathImg"
              class="card-img-top"
              :alt="producto.nombre"
            />
            <div class="card-body">
              <h5 class="card-title">{{ producto.nombre }}</h5>
              <p class="card-text">
                {{ producto.descripcionCorta }}
              </p>

              <div>
                <button
                  class="btn btn-primary"
                  data-bs-toggle="modal"
                  data-bs-target="#miModal"
                  :data-producto-id="producto.id"
                  @click="mostrar"
                >
                  Ver detalles
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Modal -->
    <div
      class="modal fade"
      id="miModal"
      tabindex="-1"
      aria-labelledby="miModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="miModalLabel">
              {{ currentProducto.nombre }}
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <p>
              <span>Descripción: </span>{{ currentProducto.descripcionCorta }}
            </p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Close
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      productos: [
        {
          id: 1,
          nombre: "Zapatillas",
          descripcionCorta: "Descripción 1",
          pathImg: "./img/imagen1.jpg",
        },
        {
          id: 2,
          nombre: "Zapatillas",
          descripcionCorta: "Descripción 2",
          pathImg: "./img/imagen2.jpg",
        },
        {
          id: 3,
          nombre: "Zapatillas",
          descripcionCorta: "Descripción 3",
          pathImg: "./img/imagen3.jpg",
        },
      ],
      currentProducto: {},
    };
  },
  methods: {
    mostrar: function (event) {
      let element = event.target;
      let productoId = element.dataset.productoId;

      //buscar elemento dentro del array de productos
      let foundProducto = this.productos.find(
        (producto) => producto.id == productoId
      );

      if (foundProducto) {
        this.currentProducto = foundProducto;
      } else {
        alert("Producto no encontrado.");
      }
    },
  },
};
</script>

<style scoped>
h1{
  padding-bottom: 40px;
  color: cadetblue;
}
</style>
