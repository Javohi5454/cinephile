<template>
    <div class="search container">
        <input type="text" class="search-input" placeholder="Найти фильм, сериал..." v-model="value">
        
        <div class="search-items">
            <div class="contentinfo-card"  v-for="(item, ind) in multiDate" :key="ind" :item="item">
                <img :src="imgUrlOriginal + item.backdrop_path" alt="" class="contentinfo-card__img" v-if="item.backdrop_path != null">
                <img :src="imgUrlOriginal + item.poster_path" alt="" class="contentinfo-card__img" v-else>
                <RouterLink :to="`/${item.media_type == 'movie' ? 'films' : 'serials'}/` + item.id" class="contentinfo-card__link">
                    {{ item.title ? item.title : item.name }}
                </RouterLink>
            </div>
        </div>
        
    </div>
</template>

<script>
import { mapState} from 'vuex'
export default {
    data() {
        return {
            value: ''
        }
    },
    watch: {
        value(){
            // console.log(this.value);
            // console.log(this.$store);
            this.$store.dispatch('search/getMultiSearch', this.value);
            
        }
    },
    computed: {
        ...mapState(['imgUrlOriginal']),
        multiDate(){
            return this.$store.state.search.searchData
        }
    },
}
</script>