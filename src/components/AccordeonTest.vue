<template>
    <div class="container">
        <div class="block" v-for="item in list" :key="item.id">
            <div class="block__container">
                <div class="block__header" @click="showText(item.id)">
                    <div class="block__title">
                        {{ item.title }}
                    </div>
                    <div
                        :class="
                            item.id === questionId && open
                                ? 'block__svg block__svg_active'
                                : 'block__svg'
                        "
                    >
                        <svg
                            width="12"
                            height="8"
                            viewBox="0 0 12 8"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                d="M1 1L6 6L11 1"
                                stroke="#0D2A54"
                                stroke-width="2"
                            />
                        </svg>
                    </div>
                </div>
            </div>
            <slide-up-down
                :duration="500"
                v-model="active"
                v-if="item.id === questionId"
            >
                <div class="block__content content">
                    <div class="content__container">
                        <div class="content__title">
                            {{ item.subtitle }}
                        </div>
                        <div class="content__svg">
                            <svg
                                width="12"
                                height="8"
                                viewBox="0 0 12 8"
                                fill="none"
                                xmlns="http://www.w3.org/2000/svg"
                            >
                                <path
                                    d="M1 1L6 6L11 1"
                                    stroke="#2B41B7"
                                    stroke-width="2"
                                />
                            </svg>
                        </div>
                    </div>

                    <ul class="content__list">
                        <li
                            class="content__item"
                            v-for="elem in item.items"
                            :key="elem.id"
                        >
                            <div class="content__circel"></div>
                            <div class="content__text">
                                {{ elem.text }}
                            </div>
                        </li>
                    </ul>
                </div>
            </slide-up-down>
        </div>
    </div>
</template>

<script setup>
import SlideUpDown from "vue3-slide-up-down";

import { ref } from "vue";
const active = ref(false);
const questionId = ref(0);
const open = ref(false);

const showText = (id) => {
    questionId.value = id;
    active.value = !active.value;
    open.value = !open.value;
};

const list = [
    {
        id: 1,
        title: "The analysis",
        subtitle: "To take into account on user level data",
        items: [
            {
                id: 2,
                text: "Do you have one user in more than one variant of the same AB test?",
            },
            {
                id: 3,
                text: "Are you users actually getting the treatment we expect them to get?",
            },
            {
                id: 4,
                text: "Do we have enough users in our AB test? Are those users representative for the total population?",
            },
        ],
    },
    {
        id: 5,
        title: "To take into account on user level data",
        subtitle: "To take into account on user level data",
        items: [
            {
                id: 6,
                text: "Do you have one user in more than one variant of the same AB test?",
            },
            {
                id: 7,
                text: "Are you users actually getting the treatment we expect them to get?",
            },
            {
                id: 8,
                text: "Do we have enough users in our AB test? Are those users representative for the total population?",
            },
        ],
    },
    {
        id: 9,
        title: "Our data",
        subtitle: "To take into account on user level data",
        items: [
            {
                id: 10,
                text: "Do you have one user in more than one variant of the same AB test?",
            },
            {
                id: 11,
                text: "Are you users actually getting the treatment we expect them to get?",
            },
            {
                id: 12,
                text: "Do we have enough users in our AB test? Are those users representative for the total population?",
            },
        ],
    },
];
</script>

<style lang="scss" scoped>
@import "@/assets/css/mixins";
.container {
    margin: 32px 8px;
    border-radius: 8px;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.02),
        0px 4px 17px rgba(0, 0, 0, 0.14), 0px 4px 22px rgba(0, 0, 0, 0.12);
    // height: 100vh;
}

.block {
    &__container {
        width: 100%;

        &::after {
            display: block;
            content: "";
            height: 1px;
            width: 100%;
            background-color: #d0dbf1;
        }
    }
    &__header {
        padding: 16px 26px 16px 16px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    &__title {
        font-weight: 800;
        font-size: 16px;
        line-height: 24px;
        color: #0d2a54;
    }
    &__svg {
        transition: transform 0.5s;

        &_active {
            transform: rotate(180deg);
        }
    }
    &__content {
        background-color: #faf8f6;
        padding: 16px;
    }
}

.content {
    &__container {
        display: flex;
        justify-content: space-between;
        gap: 7px;
    }

    &__list {
        display: flex;
        flex-direction: column;
        gap: 8px;
    }

    &__title {
        font-weight: 800;
        font-size: 16px;
        line-height: 24px;
        color: #2b41b7;
    }

    &__svg {
        margin-right: 10px;
        transform: rotate(180deg);
        display: flex;
        align-items: end;
    }

    &__item {
        display: flex;
        align-items: start;
    }

    &__text {
        flex-basis: auto;
        color: #0d2a54;
        font-weight: 600;
        font-size: 14px;
        line-height: 24px;
    }

    &__circel {
        box-sizing: border-box;
        flex-shrink: 0;
        margin: 10px 10px 0 0;
        width: 12px;
        height: 12px;
        border: 2px solid #2b41b7;
        border-radius: 50%;
    }
}

@include desc {
    .container {
        width: 600px;
        margin: 152px auto;
    }

    .block {
        &__header {
            padding: 24px 34px 24px 24px;
        }

        &__content {
            padding: 24px;
        }
    }

    .content {
        &__item {
            margin-right: 36px;
        }
    }
}
</style>
