<template>
    <v-card :to="'/detail/' + item.id">
        <v-img src="twitch-logo.png">
        </v-img>
        <v-card-title class="justify-center">{{item.attributes.name}}</v-card-title>
        <v-card-actions class="justify-center">
            <!-- <v-btn>
                {{item.attributes.price}} {{item.attributes.currency}}
            </v-btn> -->
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    props:{
        item: {}
    }
}
</script>
