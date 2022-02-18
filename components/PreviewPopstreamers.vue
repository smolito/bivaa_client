<template>
    <v-card
    :to="'/detail/' + popstreamer.id"
    width="350"
    >
        <v-img
        src="twitch-logo.png"
        height="200"
        >
        </v-img>
        <v-card-title class="justify-center">{{popstreamer.name}}</v-card-title>
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
        popstreamer: {}
    }
}
</script>
