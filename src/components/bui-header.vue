<template>
    <div :style="{'background-color':backgroundColor}">

        <div style="height: 40px;" v-if="iosFixed"></div>

        <div class="bui-header" :style="{'height':height}">
            <div class="bui-header-left" :style="{'height':height}">
                <div v-if="leftItem" @click="_leftClick($event)" class="flex-row column-center-top hot" :style="{'height': height}">
                    <bui-icon @click="_leftClick($event)" :activeColor="activeColor"
                              v-if="leftItem.icon||leftItem.icons" :name="leftItem.icon||leftItem.icons" :size="iconSize"
                              :color="iconColor"></bui-icon>
                    <text :style="{'color':textColor,'color:active':activeColor,'margin-left':'10px'}" v-if="leftItem.text"
                          class="bui-header-text" :value="leftItem.text"></text>
                </div>
                <slot name="left"></slot>
            </div>

            <div class="bui-header-main">
                <div :style="{width:maxTitleWidth}" v-if="title!==''">
                    <text :value="title" class="bui-header-title" :style="{'color':textColor}" @click="_centerClick($event)">
                    </text>
                </div>
                <slot name="center"></slot>
            </div>

            <div class="bui-header-right" :style="{'height':height}">
                <div v-if="rightItem" @click="_rightClick($event)" class="flex-row column-center-top hot" :style="{'height': height}">
                    <bui-icon @click="_rightClick($event)" :activeColor="activeColor" v-if="rightItem.icon||rightItem.icons"
                              :name="rightItem.icon||rightItem.icons" :size="iconSize" :color="iconColor"></bui-icon>
                    <text :style="{'color':textColor,'color:active':activeColor,'margin-left':'10px'}"
                          v-if="rightItem.text" class="bui-header-text" :value="rightItem.text"></text>
                </div>
                <slot name="right"></slot>
            </div>

        </div>
    </div>
</template>
<style lang="sass" src="../css/header.scss"></style>
<style lang="sass" src="../css/layout.scss"></style>

<script>
    var defaultItem = {
        icon: '',
        icons: '',
        text: ''
    };
    var platform = weex.config.env.platform.toLowerCase();
    module.exports = {
        data(){
            return{
                activeColor:"#b9c2cf"
            }
        },
        props: {
            title: {
                type: String,
                default: ""
            },
            leftItem: {
                type: Object,
                default: ""
            },
            rightItem: {
                type: Object,
                default: ""
            },
            textColor: {
                type: String,
                default: "#ffffff"
            },
            iconColor: {
                type: String,
                default: "#ffffff"
            },
            iconSize: {
                type: String,
                default: "48px"
            },
            backgroundColor: {
                type: String,
                default: "#4ca4fe"
            },
            height: {
                type: String,
                default: "90px"
            },
            maxTitleWidth: {
                type: String,
                default: "400px"
            },
            useDefaultReturn: {
                type: Boolean,
                default: true
            },
        },
        computed: {
            iosFixed () {
                return platform === "ios";
            }
        },
        methods: {
            _leftClick (e) {
                if (this.useDefaultReturn) {
                    this.$pop();
                }
                this.$emit('leftClick', e);
            },
            _rightClick (e) {
                this.$emit('rightClick', e);
            },
            _centerClick (e) {
                this.$emit('centerClick', e);
            }
        }
    }
</script>