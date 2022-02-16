<template>
    <v-row>
        <v-col cols="auto" sm="6" lg="3" md="4" v-for="item in items" :key="item.id">
            <Preview :item="item"></Preview>
        </v-col>
    </v-row>
</template>

<script>
import Preview from "../components/Preview";
export default {
    components: {Preview},
    data() {
        return {
            items: []
        }
    },
    async mounted() {
        const res = await this.$axios.get('/items');
        console.log(res.data);
        this.items = res.data;
    }
}
</script>
