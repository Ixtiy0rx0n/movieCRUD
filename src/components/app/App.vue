<template>
    <div class="app font-monospace">
        <div class="content">
            <AppInfo :allMoviesCount="movies.length" 
            :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
            <div class="search-panel">
                <SearchPanel />
                <AppFilter />
            </div>
            <MovieList 
            :movies="movies" 
            @onToggle="onToggleHandler"
            @onRemove = "onOnRemoveHandler"
            />
            <MovieAddForm @createMovie="createMovie" />
        </div>
    </div>
</template>

<script>
import AppInfo from '@/components/app-info/AppInfo.vue'
import SearchPanel from '../search-panel/SearchPanel.vue';
import AppFilter from '../app-filter/AppFilter.vue';
import MovieList from '../movie-list/MovieList.vue';
import MovieAddForm from '../movie-add-from/MovieAddForm.vue';


export default {
    components: {
        AppInfo,
        SearchPanel,
        AppFilter,
        MovieList,
        MovieAddForm,
    },
    data() {
        return {
            movies: [
                {
                    name: 'Titanik',
                    view: 811,
                    favourite: false,
                    like: false,
                    id: 1,
                },
                {
                    name: 'Scarface',
                    view: 356,
                    favourite: false,
                    like: true,
                    id: 2,
                },
                {
                    name: 'Cho`qintirgan ota-1',
                    view: 976,
                    favourite: false,
                    like: false,
                    id: 3,
                },
                {
                    name: 'Oushenning do`sti',
                    view: 546,
                    favourite: true,
                    like: true,
                    id: 4,
                },
                {
                    name: 'Wednesday',
                    view: 842,
                    favourite: true,
                    like: true,
                    id: 5,
                }
            ]
        }
    },
    methods: {
        createMovie(item) {
            this.movies.push(item)
        },
        onToggleHandler({id, prop}) {
			this.movies = this.movies.map(item => {
				if (item.id == id) {
					return {...item, [prop]: !item[prop]}
				}
				return item
			})
		},
        onOnRemoveHandler(id){
            this.movies = this.movies.filter(c => c.id !== id)
        }
    
    }
}
</script>

<style>
.app {
    height: 100vh;
    color: #000;
}

.content {
    width: 1000px;
    min-height: 700px;
    background-color: #fff;
    margin: 0 auto;
    padding: 5rem 0;
}

.search-panel {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>