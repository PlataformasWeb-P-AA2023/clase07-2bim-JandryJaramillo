<template>
    <div class="pt-5">
        <form @submit.prevent="update" method="post">
            <div class="form-group">
                <label for="nombre">Nombre</label>
                <input
                    type="text"
                    class="form-control"
                    id="nombre"
                    v-model="estudiante.nombre"
                    v-validate="'required'"
                    name="nombre"
                    placeholder="Ingrese nombre"
                    :class="{'is-invalid': errors.has('estudiante.nombre') && submitted}">
                <div class="invalid-feedback">
                    Please provide a valid name.
                </div>
            </div>
            <div class="form-group">
                <label for="direccion">Direccion</label>
                <textarea
                    name="direccion"
                    class="form-control"
                    id="direccion"
                    v-validate="'required'"
                    v-model="estudiante.direccion"
                    cols="30"
                    rows="2"
                    :class="{'is-invalid': errors.has('estudiante.direccion') && submitted}">
                  </textarea>
                <div class="invalid-feedback">
                    Please provide a valid description.
                </div>
            </div>
            <div class="form-group">
                <label for="ciudad">ciudad</label>
                <textarea
                    name="ciudad"
                    class="form-control"
                    id="ciudad"
                    v-validate="'required'"
                    v-model="estudiante.ciudad"
                    cols="30"
                    rows="2"
                    :class="{'is-invalid': errors.has('estudiante.ciudad') && submitted}">
                  </textarea>
                <div class="invalid-feedback">
                    Please provide a valid description.
                </div>
            </div>
            <div class="form-group">
                <label for="tipo">tipo</label>
                <textarea
                    name="tipo"
                    class="form-control"
                    id="tipo"
                    v-validate="'required'"
                    v-model="estudiante.tipo"
                    cols="30"
                    rows="2"
                    :class="{'is-invalid': errors.has('estudiante.tipo') && submitted}">
                  </textarea>
                <div class="invalid-feedback">
                    Please provide a valid description.
                </div>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
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
                url: '',
            },
            submitted: false
        }
    },
    mounted() {
        axios.get(this.$route.params.id)
            .then( response => {
                console.log(response.data)
                this.estudiante = response.data
            });
    },
    methods: {
        update: function (e) {
            this.$validator.validate().then(result => {
                this.submitted = true;
                if (!result) {
                    return;
                }
                axios.put((this.$route.params.id),
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
