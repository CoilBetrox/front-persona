<template>
    <div id="tabla-usuarios">
        <div v-if="!usuarios.length" class="alert alert-info" role="alert">
            No se han agregado usuarios
        </div>
        <table class="table">
            <thead>
                <tr>
                    <!--<th>Id</th> -->
                    <th>Nombre</th>
                    <th>Direccion</th>
                    <th>Edad</th>
                    <th>Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="usuario in usuarios" :key="usuario.id">
                    <!--
                    <td v-if="editando === usuario.id">
                        <input type="text" class="form-control" v-model="usuario.id" />
                    </td>
                    <td v-else>
                        {{ usuario.id}} 
                    </td>
                    -->
                    <td v-if="editando === usuario.id">
                        <input type="text" class="form-control" v-model="usuario.nombre" />
                    </td>
                    <td v-else>
                        {{ usuario.nombre }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <input type="text" class="form-control" v-model="usuario.direccion" />
                    </td>
                    <td v-else>
                        {{ usuario.direccion }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <input type="number" class="form-control" v-model="usuario.edad" />
                    </td>
                    <td v-else>
                        {{ usuario.edad }}
                    </td>
                    <td v-if="editando === usuario.id">
                        <button class="btn btn-success" @click="guardarUsuario(usuario)">💾 Guardar</button>
                        <!--<button class="btn btn-success" @click="$emit('actualizar-usuario', usuario)">💾 Guardar</button>-->
                        <button class="btn btn-secondary ml-2" @click="cancelarEdicion(usuario)">❌ Cancelar</button>
                    </td>
                    <td v-else>
                        <button class="btn btn-info" @click="editarUsuario(usuario)">✏️ Editar</button>
                        <button class="btn btn-danger ml-2" @click="$emit('eliminar-usuario', usuario)">🗑️ Eliminar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    </template>
    <script>
      export default {
        name: 'tabla-usuarios',
        props: {
           usuarios: Array,
        },
        data() {
            return {
                editando: null,
            }
        },
        methods: {
            editarUsuario(usuario) {
                this.usuarioEditado = Object.assign({}, usuario);
                this.editando = usuario.id;
            },
            guardarUsuario(usuario) {
                if (!usuario.nombre.length || !usuario.direccion.length || !usuario.edad) {
                    return;
                }
                this.$emit('actualizar-usuario', usuario);
                this.editando = null;
            },
            cancelarEdicion(usuario) {
                Object.assign(usuario, this.usuarioEditado);
                this.editando = null;
            }
        }
      }
    </script>