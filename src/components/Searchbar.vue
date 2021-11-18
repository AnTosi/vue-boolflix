<template>
    <div class="searchbar">
      <input @keyup.enter="$emit('search', searchText)" v-model="searchText" type="text" placeholder="Inserisci una ricerca">
      <button @click="$emit('search', searchText)"><i class="fas fa-search"></i></button>
    </div>
</template>

<script>
export default {
    name: 'Searchbar',
    data() {
        return {
            searchText: ""
        };
    }
}
</script>