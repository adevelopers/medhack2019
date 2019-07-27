<template>
    <div class="call-component">
        <a class="btn" v-on:click="goBack()">Назад</a>
        <a class="btn" v-on:click="callClick()">Start</a>
        <div class="layout" >
            <div class="call">
                <div class="call-name">Call name</div>
                <div class="call-video">
                    <iframe src="https://appr.tc/r/31337" width=600px height=400px allow="geolocation; microphone; camera" scrolling="no">
                        <p>Your browser does not support iframes.</p>
                    </iframe>
                </div>
            </div>
            <div class="log">
                <textarea class="call-note" cols="40" rows="3" v-on:keyup.enter="addNote" v-model="currentMessage">
                </textarea>
                <ul class="notes" >
                    <li class="doctor-note" v-for="note in notes.slice().reverse()" >
                        <div class="note-date">{{note.createDate.getHours()}}:{{note.createDate.getMinutes()}}</div>
                        <div class="note-text">{{note.text}}</div>
                    </li>
                </ul>
            </div>
            <div class="some">
                Карточка пациента
            </div>
        </div>
    <!-- Begin Fresh Tilled Soil Video Chat Embed Code -->
    <!--    <div id="freshtilledsoil_embed_widget" class="video-chat-widget"></div>-->
    <!--    <script id="fts" src="http://freshtilledsoil.com/embed/webrtc-v5.js?r=FTS0316-CZ6NqG97"></script>-->
    <!-- End Fresh Tilled Soil Video Chat Embed Code -->
    </div>
</template>

<script>
    export default {
        name: "CallWindow",
        data() {
            return {
                currentMessage: "",
                notes: []
            }
        },
        methods: {
            goBack() {
                this.$router.push('/')
            },
            addNote() {
                let newNote = {
                    createDate: new Date(),
                    text: this.currentMessage,
                } ;
                this.notes.push(newNote)
                this.currentMessage = ""
            },
            callClick() {
                
            }
        }
    }
</script>

<style scoped>
    .btn {
        width: 300px;
        height: 40px;
        font-weight: bold;
        color: white;
        background-color: blueviolet;
        padding: 10px;
        margin-right: 20px;
    }

    .call-video {
        text-align: left;
        width: 600px;
    }

    .layout {
        display: flex;
    }

    .log {
        padding: 20px;
    }

    .notes {
        list-style: none;
    }
    .doctor-note {
        text-align: left;
        margin: 0px;
        padding: 10px;
        font-weight: bold;
    }

    .note-date {
        color: #ccc;

    }

</style>