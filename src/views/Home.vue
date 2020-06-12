<template>
    <v-container class="bg">
        <v-card class="info ml-md-1 mt-md-2 mb-2 mb-md-0">
            <v-container class="Home_info display-1">
                UT ESS Srama Section
            </v-container>
        </v-card>
        <v-card class="info ml-md-1 mt-md-2 mb-2 mb-md-0">
             <v-container class="Home_info">
                <v-flex align=left>
                    <v-list-item align=left>
                        東京大学ESSドラマセクション（通称ドラセク）は
                        東京大学の英語サークル「東京大学ESS」の英語劇部門です。
                        団員は全て東京大学の学生から構成され、
                        駒場キャンパスを拠点に活動しています。
                    </v-list-item>
                    <v-list-item align=left>
                        年に2回の対外公演および１回の内部公演を通じて、
                        演劇の楽しさに加え、他の学生演劇と一味違った
                        英語劇」ならではの魅力を追及しています。
                        対外公演は東京大学駒場Ⅰキャンパス内の
                        「教養学部多目的ホール」通称「駒場小空間」にて行い、
                        全公演入場無料カンパ制となっております。
                    </v-list-item>
                    <v-list-item align=left>
                        皆様のご来場をお待ちしております。
                    </v-list-item>
                </v-flex>
            </v-container>
        </v-card>
  </v-container>
</template>

<script>
/* eslint camelcase: "off" */
// @ is an alias to /src

export default {
    name: 'Home',
    components: {
    },
    data () {
        return {
            info_dialog: null,
            info: {},
            items:  [
            ]
        }
    },
    methods: {
        open_info (info) {
            this.info = info;
            this.info_dialog = true;
        }
    },
    mounted () {
        this.axios.get('https://fwnr71w8e0.execute-api.us-east-2.amazonaws.com/default/getKibelaPages?action=bundle&path=Info')
            .then(response => {
                let year = 3000;
                for (const edge of response.data.notes.edges) {
                    const title_parse = edge.node.title.match(/(?<year>\d\d\d\d)-(?<date>\d\d-\d\d)\s*(?<title>.*)/);
                    if (title_parse === null) {
                        continue;
                    }
                    console.log(title_parse.groups);
                    if (Number(title_parse.groups.year) < year) {
                        this.items.push({
                            header: title_parse.groups.year
                        });
                        year = Number(title_parse.year);
                    }
                    this.items.push({
                        date: title_parse.groups.date,
                        title: title_parse.groups.title,
                        active: false,
                        content: edge.node.content
                    });
                }
            });
    }
}
</script>

<style scoped>
.info {
    overflow-y: scroll;
    max-height: 45vh;
}

/*スクロールバー全体*/
::-webkit-scrollbar {
    width: 7px;
    background-color: white;
}

/*スクロールバーの軌道*/
::-webkit-scrollbar-track {
    border-radius: 5px;
}

/*スクロールバーの動く部分*/
::-webkit-scrollbar-thumb {
    background-color: gray;
    border-radius: 5px;
    box-shadow:0 0 0 1px rgba(255, 255, 255, 1.0);
}

.bg {
    width: 100%;
    height: 100%;
    opacity: 0.8;
    top: 0;
    left: 0;
    background-position: center center;
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;
    background-image: url("~@/assets/les_miserables.jpg");
}

.Home_info{
    background-color: white;
}

</style>
