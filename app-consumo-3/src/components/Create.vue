<template>
    <div class="pt-5">
        <form @submit.prevent="create" method="post">
            <div class="form-group">
                <label for="nombre">Nombre</label>
                <input
                    type="text"
                    class="form-control"
                    id="nombre"
                    v-model="estudiante.nombre"
                    v-validate="'required'"
                    name="nombre"
                    placeholder="Ingres su nombre"
                    :class="{'is-invalid': errors.has('estudiante.nombre') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid name.
                </div>
            </div>

            <div class="form-group">
                <label for="direccion">Direccion</label>
                <input
                    type="text"
                    class="form-control"
                    id="nombre"
                    v-model="estudiante.direccion"
                    v-validate="'required'"
                    name="direccion"
                    placeholder="Ingres su direccion"
                    :class="{'is-invalid': errors.has('estudiante.direccion') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid direccion.
                </div>
            </div>

            <div class="form-group">
                <label for="ciudad">Ciudad</label>
                <input
                    type="text"
                    class="form-control"
                    id="ciudad"
                    v-model="estudiante.ciudad"
                    v-validate="'required'"
                    name="apellido"
                    placeholder="Ingres su cédula"
                    :class="{'is-invalid': errors.has('estudiante.ciudad') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid ciudad.
                </div>
            </div>

            <div class="form-group">
                <label for="tipo">Tipo</label>
                <input
                    type="text"
                    class="form-control"
                    id="tipo"
                    v-model="estudiante.tipo"
                    v-validate="'required'"
                    name="apellido"
                    placeholder="Ingres su tipo"
                    :class="{'is-invalid': errors.has('estudiante.tipo') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid tipo.
                </div>
            </div>
            <button type="submit" class="btn btn-primary">Crear</button>
        </form>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    data() {
        return {
            estudiante: {
                nombre: '',
                direccion: '',
                ciudad: '',
                tipo: '',
            },
            submitted: false
        }
    },
    methods: {
        create: function (e) {
            this.$validator.validate().then(result => {
                this.submitted = true;
                if (!result) {
                    return;
                }
                console.log(this.ciudad)
                axios.post('http://127.0.0.1:8000/edificios/',
                        this.estudiante
                    )
                    .then(response => {
                        this.$router.push('/');
                    })
            });
        }
    },
}
</script>
