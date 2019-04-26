<template>
    <div class="emoji-container" :style="style">
        <div class="recent-area">
            <div class="flex flex-col">
                <div class="text-sm text-left col-white">Recently Used</div>
                <div class="emojisRecentUI">
                    <img class="emoji grow" :src=emoji.source v-for="emoji in recentlyUsedList" v-bind:key="emoji.id"
                         v-on:click="getSelected(emoji)">
                </div>
            </div>
            <div id="wrap">

                <input v-model="typed" id="searchUIx" name="search" type="text"
                       placeholder="Search Reaction?"><input id="search_submit" type="submit">

            </div>
        </div>
        <div class="emoji-area">
            <div class="emojisUI">
                <img :alt=emoji.tag class="emoji grow" :src=emoji.source v-for="emoji in filteredList" v-bind:key="emoji.id"
                     v-on:click="getSelected(emoji)">
            </div>

        </div>
    </div>
</template>

<script>
    export default {
        name: 'Emoji',
        props: {
            emojis: {
                type: Array
            },
            recently_used: {
                type: Array
            },
            background: {
                type: String
            }
        },
        data: function () {
            return {
                filtered: this.emojis,
                typed: "",

            };
        },
        computed: {
            style: function () {
                let col = this.background ? this.background : 'grey';
                return 'background-color:' + col + "!important;";
            },
            filteredList() {
                return this.emojis.filter(emoji => {
                    if (this.typed.length === 0) return true;

                    if (emoji['keywords'].length === 0 && this.typed.length > 0) return false;

                    let match = false;

                    for (let i = 0; i < emoji['keywords'].length; i++) {
                        let runSearch = emoji['keywords'][i].toString().toUpperCase().match(this.typed.toString().toUpperCase());
                        match = (runSearch.isArray() && runSearch.length > 0);
                        if (match) break;
                    }
                    return match;
                })
            }, recentlyUsedList() {
                return this.recently_used;
                // return this.recently_used.filter(emoji => {
                //
                //     for (var i = 0; i < recent.length; i++) {
                //         var one = recent[i];
                //         return emoji.id === one;
                //     }
                //
                //
                // })
            }
        },
        mounted: function () {
            // if (localStorage.rannton_emoji !== "" || localStorage.rannton_emoji) {
            //     this.recently_used = JSON.parse(localStorage.rannton_emoji)
            // }
            // else {
            //     localStorage.rannton_emoji = [];
            // }
            //this.filtered = this.emojis;
            // let col=this.background?this.background:'grey';
            // console.log('background-color:' + col + "!important;")
        },
        methods: {
            getRecentEmoji: function () {
                return [];
            },
            getSelected: function (emoji) {
                //var recent = this.getRecentEmoji();

                // this.saveRecentEmoji(emoji.id);
                this.$emit('onEmojiClicked', emoji)
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    ::-webkit-input-placeholder { /* Chrome/Opera/Safari */
        color: lightgrey;
    }

    ::-moz-placeholder { /* Firefox 19+ */
        color: lightgrey;
    }

    :-ms-input-placeholder { /* IE 10+ */
        color: lightgrey;
    }

    :-moz-placeholder { /* Firefox 18- */
        color: lightgrey;
    }

    .emoji {
        width: 65px;
        height: 65px;
        float: left;
        margin-right: 12px;
        margin-bottom: 8px;
        object-fit: contain;
    }

    .grow {
        transition: all .2s ease-in-out;
    }

    .grow:hover {
        transform: scale(1.1);
    }

    .recent-area {
        height: 20%;
        position: relative;
        padding: 15px 25px;
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
    }

    .emojisRecentUI {
        height: 90%;
        margin-top: 10px;
    }

    .emojisRecentUI img {
        width: 45px;
        height: 45px;
    }

    .emojisUI {
        margin-top: 10px;
        height: 98%;
        background: transparent;
        padding: 10px 20px;
        overflow-y: scroll;
        margin-left: 10px;
    }

    .emoji-area {
        height: 80%;

        position: relative;

        /*display: flex;*/
        border-bottom-left-radius: inherit;
        border-bottom-right-radius: inherit;

    }

    .emoji-container {
        width: 100%;

        flex-direction: column;
        min-height: 350px;
        height: 100%;
        border-radius: 15px;
        background: grey;
        display: flex;
        flex: 1;
    }

    #wrap {
        width: 30%;
        top: 25px;
        display: inline-block;
        right: 30px;
        height: 30px;
        float: right;
        padding: 0;
        position: absolute;
    }

    input[type="text"] {
        height: 28px;
        font-size: .9em;
        display: inline-block;
        font-weight: 100;
        border: none;
        outline: none;
        color: #555;
        padding: 3px;
        padding-right: 30px;
        width: 0px;
        position: absolute;
        top: 0;
        right: 0;
        color: white;
        background: none;
        z-index: 3;
        transition: width .4s cubic-bezier(0.000, 0.795, 0.000, 1.000);
        cursor: pointer;
    }

    input[type="text"]:focus:hover {
        border-bottom: 1px solid #BBB;
    }

    input[type="text"]:focus {
        width: 100%;
        z-index: 1;
        border-bottom: 1px solid #BBB;
        cursor: text;
    }

    input[type="submit"] {
        height: 21px;
        width: 21px;
        display: inline-block;
        color: red;
        float: right;
        background: transparent;
        background-image: url("data:image/svg+xml,%0A%3Csvg width='20px' height='20px' viewBox='0 0 20 20' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Cg id='Icons' stroke='none' stroke-width='1' fill='none' fill-rule='evenodd'%3E%3Cg id='Utils' transform='translate(-260.000000, -140.000000)' fill='%23FFFFFF'%3E%3Cg id='icons' transform='translate(20.000000, 20.000000)'%3E%3Cpath d='M260.0026,138.5855 L258.5886,139.9995 L254.3456,135.7575 L255.7596,134.3425 L260.0026,138.5855 Z M248.0026,133.9995 C244.6946,133.9995 242.0026,131.3085 242.0026,127.9995 C242.0026,124.6915 244.6946,121.9995 248.0026,121.9995 C251.3106,121.9995 254.0026,124.6915 254.0026,127.9995 C254.0026,131.3085 251.3106,133.9995 248.0026,133.9995 L248.0026,133.9995 Z M248.0026,119.9995 C243.5846,119.9995 240.0026,123.5815 240.0026,127.9995 C240.0026,132.4175 243.5846,135.9995 248.0026,135.9995 C252.4206,135.9995 256.0026,132.4175 256.0026,127.9995 C256.0026,123.5815 252.4206,119.9995 248.0026,119.9995 L248.0026,119.9995 Z' id='search_left-%5B%231504%5D'%3E%3C/path%3E%3C/g%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
        background-repeat: no-repeat;
        background-size: contain;
        text-indent: -10000px;
        border: none;
        position: absolute;
        top: 0;
        right: 0;
        z-index: 2;
        cursor: pointer;
        opacity: 1;
        cursor: pointer;
        transition: opacity .4s ease;
    }

    input[type="submit"]:hover {
        opacity: 1;
    }

    .flex {
        display: flex;
        flex: 1;
    }

    .flex-c {
        justify-content: center;
    }

    .flex-c-m {
        justify-content: center;
        align-content: center;
        align-items: center;
    }

    .flex-m {
        align-content: center;
        align-items: center;
    }

    .flex-sb {
        display: flex;
        justify-content: space-between;
    }

    .flex-col {
        flex-direction: column;
    }

    .text-left {
        text-align: left;
    }

    .text-sm {
        font-family: inherit !important;
        font-size: .7em;
    }

    .col-white {
        color: white;
    }
</style>
