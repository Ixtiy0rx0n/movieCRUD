<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex" @submit.prevent>
            <input type="text" class="form-control new-movie-label" placeholder="Qanday kino?" :value="name"
                @input="name = $event.target.value" />

            <input type="Number" class="form-control new-movie-label" placeholder="Nechi marotaba ko'rilgan"
                :value="view" @input="view = $event.target.value" />

            <button class="btn btn-outline-dark" type="submit" @click="addMovie">
                Qo'shish
            </button>
        </form>
    </div>
</template>

<script>
import MovieList from '../movie-list/MovieList.vue';

export default {
    data() {
        return {
            name: '',
            view: ''
        }
    },
    methods: {
        addMovie() {
            if(!this.name || !this.view) return null
            const newMovie = {
                name: this.name,
                view: this.view,
                favourite: false,
                like: false,
                id: Date.now()
            }
            this.$emit("createMovie", newMovie)
            this.name = ""
            this.view = ""
        },
    }
}
</script>

<style>
.movie-add-form {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>