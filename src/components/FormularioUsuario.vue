<template>
    <div id="formulario-usuario">
        <form @submit.prevent="enviarFormulario">
            <div class="container">
                <div class="row">
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Nombre</label>
                            <input
                                ref="nombre"
                                v-model="usuario.nombre"
                                type="text"
                                class="form-control"
                                :class="{ 'is-invalid': procesando && nombreInvalido }"
                                @focus="resetEstado"
                                @keypress="resetEstado"
                            />
                        </div>
                    </div>
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Direccion</label>
                            <input
                                v-model="usuario.direccion"
                                type="text"
                                :class="{ 'is-invalid': procesando && direccionInvalido }"
                                class="form-control"
                                @focus="resetEstado"
                            />
                        </div>
                    </div>
                    <div class="col-md-4">
                        <div class="form-group">
                            <label>Edad</label>
                            <input
                                v-model="usuario.edad"
                                type="number"
                                :class="{ 'is-invalid': procesando && edadInvalido }"
                                class="form-control"
                                @focus="resetEstado"
                            />
                        </div>
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-4">
                        <div class="form-group">
                            <button class="btn btn-primary">Añadir usuario</button>
                        </div>
                    </div>
                </div>
            </div>
            <div class="container">
                <div class="row">
                    <div class="col-md-12">
                        <div v-if="error && procesando" class="alert alert-danger" role="alert">
                            Debes rellenar todos los campos!
                        </div>
                        <div v-if="correcto" class="alert alert-success" role="alert">
                            El usuario ha sido agregada correctamente!
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </div>
    </template>
    
    <script>
    export default {
        name: 'formulario-usuario',
        data() {
          return {
                procesando: false,
                correcto: false,
                error: false,
                usuario: {
                    nombre: '',
                    direccion: '',
                    edad: '',
                }
          }
        },
        methods: {
            enviarFormulario() {
                this.procesando = true;
                this.resetEstado();
                
                // Comprobamos la presencia de errores
                if (this.nameInvalido || this.direccionInvalido || this.edadInvalido) {
                    this.error = true;
                    return;
                }
                this.$emit('crear-usuario', this.usuario);
                this.$refs.nombre.focus();
                this.error = false;
                this.correcto = true;
                this.procesando = false;
                // Restablecemos el valor de la variables
                this.usuario= {
                    nombre: '',
                    direccion: '',
                    edad: ''
                }
                console.log(this.usuario);
            },
            resetEstado() {
                this.correcto = false;
                this.error = false;
            }
        },
        computed: {
            nameInvalido() {
                return this.usuario.nombre.length < 1;
            },
            direccionInvalido() {
                return this.usuario.direccion.length < 1;
            },
            edadInvalido() {
                return this.usuario.edad < 1;
            },
        },
    }
    </script>
    
    <style scoped>
    form {
        margin-bottom: 2rem;
    }
    </style>