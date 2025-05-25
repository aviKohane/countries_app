<template id="grid">
    <div class="table-wrapper">
        <table>
            <thead>
                <tr class="header">
                    <th v-for="key in gridColumns">
                        {{ key }}
                    </th>
                </tr>
            </thead>
            <tbody class="scroll-body">
                <tr v-for="country in filteredCountries" :key="country.cca3 || country.name.common">
                    <td>
                        <div class="flag-cell">
                            <img :src="country.flags.png" :alt="country.flags.alt || 'Flag of ' + country.name.common" width="50" height="30">
                        </div>
                        <div>

                        </div>
                    </td>
                    <td>
                        <a :href="country.maps.googleMaps">{{ country.name.common }}</a>
                    </td>
                    <td>
                        {{ country.capital?.[0] || 'No capital' }}
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
   
</template>

<script>
export default {
    name: 'CountriesGrid',
    props: {
        searchValue: String,
        countries:Array,
    },
    data() {
        return {
            gridColumns: ['Flag','Name', 'Capital'],
        }
    },
    computed: {
        filteredCountries() {
            const query = this.searchValue.toLowerCase().trim();
            if (query.length > 0) {
                return this.countries.filter(item =>
                    item.name.common.toLowerCase().includes(query) ||
                    item.capital?.[0].toLowerCase().includes(query));

            }
            else
                return this.countries;
        }

    },
   
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.table-wrapper {
    width: 100%;
    border: 2px solid blue;
    background-color: rgb(255, 255, 255);
    border-radius: 5px;
}

thead {
    background-color: blue;

}

table {
    width: 100%;
    border-collapse: collapse;
    table-layout: fixed;
}

.header {
    display: flex;
    justify-content: space-around;
}

th {
    position: sticky;
    top: 0;
    background-color: blue;
    color: lightgrey;
    z-index: 2;
    text-align: left;
    padding: 10px 20px;

}

td {
    color: black;
    vertical-align: middle;

}

.flag-cell {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5px
}

a {
    color: black;
}

tbody tr td {
    border: 1px solid blue;
}

.scroll-body {
    display: block;
    max-height: 73vh;
    overflow-y: overlay;
    background-color: currentColor;
}

.scroll-body tr {
    display: table;
    width: 100%;
    table-layout: fixed;
}
</style>
