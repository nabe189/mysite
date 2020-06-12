<template>
    <nav>
        <v-toolbar flat app>
            <v-toolbar-side-icon class="grey--text" @click="drawer = !drawer"></v-toolbar-side-icon>
            <v-toolbar-title>
                <span>UTESS </span>
                <span class="font-weight-light">Drama Section</span>
            </v-toolbar-title>

            <v-spacer></v-spacer>

            <v-toolbar-items class="hidden-sm-and-down">
                <v-btn class="font-weight-light" text v-for="item in items" :to="item.to" :key="item.to">{{ item.title }}</v-btn>
                <v-btn class="font-weight-light" text hover href='https://twitter.com/utessdrama'>Twitter</v-btn>
            </v-toolbar-items>

        </v-toolbar>

        <v-navigation-drawer v-model="drawer">
            <v-list-item v-for="item in items" :key="item.title" :to="item.to" link align="left">
                    <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
        </v-navigation-drawer>

    </nav>
</template>

<script>
export default {
    data () {
        return {
            drawer: false,
            items: [
                { title: 'Home', to: '/' },
                { title: 'About', to: '/about' },
                { title: 'Productions', to: '/productions' },
                { title: 'Gallery', to: '/gallery' },
                { title: 'Contact', to: '/contact' }
            ]
        }
    }
}
</script>