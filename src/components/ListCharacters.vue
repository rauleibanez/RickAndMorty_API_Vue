<template>
    <section>
	    <div class="characters">
            <div class="characters__item" v-for="character in characters" :key="character.id">
	            <!-- Write your HTML with Vue in here -->
                <CardCharacters :character = "character" />
            </div>     
	    </div>
	</section>
</template>

<script>
    import {onMounted, computed } from 'vue'
    import {useStore} from 'vuex'
    import CardCharacters from '@/components/CardCharacters'
    export default {
		// Write your Vue component logic here
        components:{
            CardCharacters
        },
        setup(){
            const store = useStore()
            const characters = computed(()=>{
                return store.state.charactersFilter
            })
            onMounted(()=>{
                store.dispatch('getCharacters')
            })
            return {
                characters
            }
        }
    }
</script>

<style lang="scss">
	/* Write your styles for the component in here */
 .characters {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 3rem;
  margin: 3rem 0;
}
</style>