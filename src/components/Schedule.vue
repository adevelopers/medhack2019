<template>
    <div class="schedule"><!-- Расписание для врача -->
        <h1>Расписание</h1>
        <h2 class="schedule-title">Сегодня</h2>
        <ul class="card-list">
            <li class="card" v-for="card, key in cards">
                <!-- Карточка приёма -->
                <div class="card-icon"></div>
                <div class="card-name">Имя: {{card.name}}</div>
                <div class="card-status">Стутс: {{card.status}}</div>
                <div class="card-diagnose">Диагноз: {{card.diagnose}}</div>
                <div class="card-buttons">
                    <a class="card-button" >Перенести</a>
                    <a class="card-button" v-on:click="call()">Звонок</a>
                </div>
                <div class="card-panel--bottom">
                    <div class="card-panel-icon icon-medcard"></div>
                    <div class="card-panel-icon icon-analize"></div>
                    <div class="card-panel-icon icon-naznacheniya" alt="Назначения"></div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: "Schedule",
        data() {
            return {
                cards: [],
                errors: []
            }
        },
        created() {
            this.getCardsDemo()
        },
        methods: {
            getCardsDemo() {
                this.cards = [
                    {
                        id: "1",
                        name:"Лупул Андрей",
                        status: "Вторичный",
                        diagnose: "Остро расператорная ангина",
                        date: "12.10.2019"
                    },
                    {
                        id: "2",
                        name:"Сказочный",
                        status: "Вторичный",
                        diagnose: "Болен",
                        date: "11.10.2019"
                    },
                    {
                        id: "3",
                        name:"Сказочный",
                        status: "Вторичный",
                        diagnose: "Болен",
                        date: "11.10.2019"
                    },
                    {
                        id: "4",
                        name:"Сказочный",
                        status: "Вторичный",
                        diagnose: "Болен",
                        date: "11.10.2019"
                    },
                    {
                        id: "5",
                        name:"Сказочный",
                        status: "Вторичный",
                        diagnose: "Болен",
                        date: "11.10.2019"
                    },
                ];
            },
            getCards() {
                axios.get('/api/cards')
                    .then(({ data }) => {
                        this.items = data.messages
                        let counter = document.getElementById("notifications_count")
                        counter.innerHTML = Object.keys(data.messages).length
                    })
                    .catch(e => {
                        this.errors.push(e)
                    })
            },
            call() {
                console.log("Query", this.$route.path);
                // location.href= "/call/";
                this.$router.push('/call')

                // this.$router.push('/calling/')
            }
        }

    }
</script>

<style scoped>
    .schedule-title {
        text-align: left;
        padding-left: 40px;
    }

    .card-list {
        list-style: none;
    }

    .card {
        font-size: 18px;
        text-align: left;
        margin-bottom: 50px;
        margin-right: 40px;
        border: 1px dotted #333;
        padding: 20px;
        height: 110px;
    }

    .card-name,
    .card-status,
    .card-diagnose
    {
        font-weight: bold;
    }

    .card-buttons {
        float: right;
    }

    .card-button {
        width: 300px;
        height: 40px;
        font-weight: bold;
        color: white;
        background-color: blueviolet;
        padding: 10px;
        margin-right: 20px;
    }

</style>