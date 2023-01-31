<template>
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200&display=swap" rel="stylesheet">
    <div class="my1920">
        <!--PACMAN + BUTTON-->
        <PacmanBlock />

        <div class="header">
            <button class="button_upper">
                <div class="text" @click="scrollMeTo(porto)">Произвести биоробота</div>
            </button>
        </div>


        <!--ФАБРИКА-->
        <FabricBlock />


        <!--КОШЕЛЕК КРИПТОВАЛЮТ-->
        <div class="koshelek" ref="porto">
            Кошелек криптовалют<br>

        </div>
        <div class="box1">
            <label class="checkbox-other">
                <input type="checkbox" @change="e => addingCount = e.target.checked ? 5 : 1">
                <span class="money5">Цыганить по 5 монет</span>
            </label>
        </div>
        <div class="getMaining">
            <div class="maining" @click="onMining">Нацыганить</div>
        </div>
        <div class="summ">
            {{ coinsCount }} biorobo {{ coinWordFrom }}
        </div>
        <div class="copy_one">
            <img v-for="i in coinsCount" :key="i" src="./assets/117.png" class="money">
        </div>

        <!--РЫНОК КОМПЛЕКТУЮЩИХ-->
        <div class="rinok">
            Рынок комплектующих

            <img src="./assets/roboBiohand.svg" class="biohand">
            <div class="biohand_bright"></div>

        </div>
        <div class="bio_text">
            Биорука
        </div>
        <div class="cost7">
            Стоимость {{ prices.hands.buy }} монет
        </div>
        <div class="icon4">
            <img src="./assets/microchip.svg" class="vector">
            <div class="vector_bright"></div>
        </div>
        <div class="micro">
            Микрочип
        </div>
        <div class="cost5">
            Стоимость {{ prices.microchips.buy }} монет
        </div>
        <div class="icon3">
            <div class="circle">
                <img src="./assets/soul.svg" class="vector2">
            </div>
        </div>
        <div class="soul">
            Душа
        </div>
        <div class="cost25">
            Стоимость {{ prices.souls.buy }} монет
        </div>
        <button class="button_fill" :disabled="coinsCount < 7" @click="coinsCount -= prices.hands.buy; store.hands++">
            <div class="text1">
                Установить
            </div>
        </button>
        <button class="button" :disabled="coinsCount < 5" @click="coinsCount -= prices.microchips.buy; store.microchips++">
            <div class="text1">
                Установить
            </div>
        </button>
        <button class="button_soul" :disabled="coinsCount < 25" @click="coinsCount -= prices.souls.buy; store.souls++">
            <div class="text1">
                Установить
            </div>
        </button>

        <!--СКЛАД-->
        <div class="sklad">
            <!-- <v-content>
                <SectionOne id="section-one" />
            </v-content> -->
            Склад
        </div>
        <!--Биорука--->
        <div class="storehouse_hand">
            Биорука
        </div>
        <div class="storehouse_cost5">
            Стоимость: {{ prices.hands.sell }} монет
        </div>
        <div class="storehouse_2_coins">
            {{ store.hands }} шт
        </div>
        <button class="button_store_bio" :disabled="store.hands <= 0">
            <div class="button_store_bio_text" @click="coinsCount += prices.hands.sell; store.hands--"
                :disabled="store.hands <= 0">
                Продать
            </div>
        </button>
        <!--Микрочип--->
        <div class="storehouse_micro">
            Микрочип
        </div>
        <div class="storehouse_cost_micro3">
            Стоимость: {{ prices.microchips.sell }} монет
        </div>
        <div class="storehouse_micro_coins">
            {{ store.microchips }} шт
        </div>
        <button class="button_store" :disabled="store.microchips <= 0">
            <div class="button_store_text" @click="coinsCount += prices.microchips.sell; store.microchips--"
                :disabled="store.microchips <= 0">
                Продать
            </div>
        </button>
        <!--Душа--->
        <div class="storehouse_soul">
            Душа
        </div>
        <div class="storehouse_cost_soul">
            Стоимость: {{ prices.souls.sell }} монет
        </div>
        <div class="storehouse_soul_coins">
            {{ store.souls }} шт
        </div>
        <button class="button_store_soul" :disabled="store.souls <= 0">
            <div class="button_store_soul_text" @click="coinsCount += prices.souls.sell; store.souls--"
                :disabled="coinsCount < 25">
                Продать
            </div>
        </button>

        <!--ПРОИЗВОДСТВО--->
        <div class="production">
            Производство
        </div>
        <!--Тип биоробота-->
        <div class="type_bio">Тип биоробота
            <!--radio тип биоробота-->
            <div class="radio_box">
                <div class="form_radio">
                    <input id="radio-1" type="radio" name="radio" v-model="robotType" value="frontend">
                    <label for="radio-1">FrontEnd</label>
                </div>
                <div class="form_radio">
                    <input id="radio-2" type="radio" name="radio" v-model="robotType" value="design">
                    <label for="radio-2">Design</label>
                </div>
            </div>
        </div>
        <div class="stabilizator">
            Стабилизатор
            <!--radio стабилизатор-->



            <div class="radio_box">
                <div class="form_radio">
                    <input id="radio-3" type="radio" name="radio2" v-model="robotGender" value="Male">
                    <label for="radio-3">Male</label>
                </div>
                <div class="form_radio">
                    <input id="radio-4" type="radio" name="radio2" v-model="robotGender" value="Famale">
                    <label for="radio-4">Famale</label>
                </div>
            </div>
        </div>
        <div class="info_needed">
            {{ robotCreateErrorText }}
        </div>

        <button class="button_create" :disabled="coinsCount < 10" @click="onRobotCreate()">
            <span class="button_create_text">
                Произвести за 10 монет
            </span>
        </button>
        <div class="money_info">
            <div v-if="robotCreatedSuccessfulyPopup">
                <div class="v-popup">
                    <div class="coin_x">
                        <button class="close" @click="robotCreatedSuccessfulyPopup = false">x</button>
                    </div>

                    <div class="for_text">
                        <div class="v-popup_header">
                            <h1>Биоробот произведен</h1>
                        </div>
                        <div class="youCant">Вы произвели биоробота
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="constructor_conteiner">

            <div class="constructor_items">
                <div v-for="i in 4" :key="i">

                    <img v-if="i <= store.hands" src="./assets/biohand_ready.png" alt />
                    <img v-else-if="i <= 4 && coinsCount >= 28" src="./assets/white_hand.png" class="inside_details"
                        alt />
                    <img v-else-if="i <= 3 && coinsCount >= 21" src="./assets/white_hand.png" class="inside_details"
                        alt />
                    <img v-else-if="i <= 2 && coinsCount >= 14" src="./assets/white_hand.png" class="inside_details"
                        alt />
                    <img v-else-if="i > store.hands" src="./assets/biohand_dark.png" class="inside_details" alt />

                </div>
            </div>
            <div class="constructor_items">
                <div v-for="i in 4" :key="i">
                    <img v-if="i <= store.microchips" src="./assets/microchip_ready.png" alt />
                    <img v-else-if="i <= 4 && coinsCount >= 20" src="./assets/microchip_white.png"
                        class="inside_details" alt />
                    <img v-else-if="i <= 3 && coinsCount >= 15" src="./assets/microchip_white.png"
                        class="inside_details" alt />
                    <img v-else-if="i <= 2 && coinsCount >= 10" src="./assets/microchip_white.png"
                        class="inside_details" alt />
                    <img v-else-if="i > store.microchips" src="./assets/microchip_dark.png" class="dark_details" alt />
                </div>
            </div>
            <div class="constructor_items">
                <div v-for="i in 1" :key="i">
                    <img v-if="i <= store.souls" src="./assets/soul_ready.png" alt />
                    <img v-else-if="coinsCount >= 25" src="./assets/soul_white.png" class="inside_details" alt />
                    <img v-else-if="i > store.souls" src="./assets/soul_dark.png" class="dark_details" alt />

                </div>
            </div>
        </div>

        <div class="Robot" :style="{
            backroundImage: 'url(' + require('./assets/33.png') + ')',
            backgroundPosition: robotBgPos
        }">
        </div>

        <!-- 
                src="./assets/robots_available.png" alt=""
                && store.hands<4 || store.microchips<2 || store.souls<1
                <img v-if="'one'" src="./assets/soul.png" alt />-->
        <div class="money_info">
            <div v-if="showMiningError">
                <div class="v-popup">
                    <div class="coin_x">

                        <button class="close" @click="showMiningError = false">x</button>

                    </div>
                    <img class="v-catalog_item" src="./assets/117.png">
                    <div class="for_text">
                        <div class="v-popup_header">
                            <h1>Количество монет<br>ограничено</h1><br>
                        </div>
                        <div class="youCant">Вы не можете нацыганить <br>более 100 biorobo монет
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>
 
<script setup>

import PacmanBlock from "./PacmanBlock/PacmanBlock.vue";
import FabricBlock from "./FabricBlock/FabricBlock.vue";
import { ref, reactive, computed } from 'vue'


const coinsCount = ref(1)
const coinWordFrom = computed(() => {
    const forms = ['монета', 'монеты', 'монет']
    const dec = Math.floor(coinsCount.value / 10) % 10
    const ones = coinsCount.value % 10
    if (dec === 1) return forms[2]
    if (ones === 1) return forms[0]
    if (ones >= 2 && ones <= 4) return forms[1]
    return forms[2]
})

const addingCount = ref(1)
const showMiningError = ref(false)

const prices = {
    hands: {
        buy: 7,
        sell: 5
    },
    microchips: {
        buy: 5,
        sell: 3
    },
    souls: {
        buy: 25,
        sell: 15
    }
}

const store = reactive({
    hands: 3,
    microchips: 2,
    souls: 0
})

const onMining = () => {
    if (coinsCount.value >= 100) {
        showMiningError.value = true
    }
    else {
        coinsCount.value = Math.min(coinsCount.value + addingCount.value, 100)
    }
}

const porto = ref(null)
const scrollMeTo = (elem) => {
    window.scrollTo(0, elem.offsetTop)
}

const robotType = ref(null)
const robotGender = ref(null)
const robotBgPos = computed(() => {
    if (!robotType.value || !robotGender.value) return '0 0'
    if (store.hands < 4 || store.microchips < 2 || store.souls == 0) {
        if (robotType.value === 'frontend') {
            if (robotGender.value === 'Male') {
                return '0 0'
            }
            else {
                return '0 0'
            }
        }
        else {
            if (robotGender.value === 'Male') {
                return '0 0'
            }
            else {
                return '0 0'
            }
        }
    }
    else if (!robotCreatedSuccessfuly.value) {
        if (robotType.value === 'frontend') {
            if (robotGender.value === 'Male') {
                return '0 0'
            }
            else {
                return '0 0'
            }
        }
        else {
            if (robotGender.value === 'Male') {
                return '0 0'
            }
            else {
                return '0 0'
            }
        }
    }
    else {
        if (robotType.value === 'frontend') {
            if (robotGender.value === 'Male') {
                return '0 0'
            }
            else {
                return '0 0'
            }
        }
        else {
            if (robotGender.value === 'Male') {
                return '0 0'
            }
            else {
                return '0 0'
            }
        }
    }
})

const robotCreateErrorText = computed(() => {
    const errors = []
    if (store.hands < 4) {
        errors.push(store.hands === 3 ? 'биомеханизма' : `${4 - store.hands} биомеханизмов`)
    }
    if (store.microchips < 2) {
        errors.push(store.microchips === 2 ? 'процессора' : `${4 - store.microchips} процессоров`)
    }
    if (store.souls < 1) {
        errors.push('души')
    }
    if (coinsCount.value < 10) {
        errors.push('денег')
    }
    if (errors.length > 0) {
        const last = errors.pop()
        if (errors.length > 0) {
            return `Не хватает ${errors.join(', ')} и ${last}`
        }
        return `Не хватает ${last}`
    }
    return ''
})
const robotCreatedSuccessfuly = ref(false)
const robotCreatedSuccessfulyPopup = ref(false)
const onRobotCreate = () => {
    if (robotCreateErrorText.value === '') {
        robotCreatedSuccessfuly.value = true
        robotCreatedSuccessfulyPopup.value = true
    }
}

</script>


<style src="./global.css">

</style> <!--Подключение css -->


