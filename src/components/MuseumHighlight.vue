<template>
    <div class="highlight">
        <div class="highlight__card">
            <div class="highlight__card__banner">
                <img class="highlight__card__banner__image"
                :src="highlightData.image || `https://source.unsplash.com/random/?astronomy,sig=${imageNum}`" />
                <div class="highlight__card__banner__shadow" />
                <p class="highlight__card__banner__title">
                    {{ highlightData.name  ?? 'Card Title' }}
                </p>
            </div>
            <div :class="`highlight__card__content ${highlightData.partner ? 'dark-theme' : ''}`">
                <div class="highlight__card__content__details">
                    <p class="highlight__card__content__details__date">
                        {{ highlightData.date ?? '' }}
                    </p>
                    <div class="highlight__card__content__details__quiz"
                    v-if="highlightData.quiz">
                        <a :href="highlightData.quiz">
                            Try the quiz!
                        </a>
                        <i class="material-symbols-outlined">arrow_forward</i>
                    </div>
                    <p class="highlight__card__content__details__period"
                    v-else-if="highlightData.period">
                        {{ highlightData.period }}
                    </p>
                    <div class="highlight__card__content__details__habitat"
                    v-else-if="highlightData.species || highlightData.location">
                        <p class="highlight__card__content__details__habitat__species">
                            {{ highlightData.species }}
                        </p>
                        <p class="highlight__card__content__details__habitat__location">
                            {{ highlightData.location }}
                        </p>
                    </div>
                </div>
                <div class="highlight__card__content__description">
                    <p>
                        {{ highlightData.description ?? '' }}
                    </p>
                </div>
                <hr class="highlight__card__content__divider"
                v-if="highlightData.news" />
                <div class="highlight__card__content__news"
                v-if="highlightData.news">
                    <p class="highlight__card__content__news__title">
                        {{ highlightData.news.title ?? '' }}
                    </p>
                    <p class="highlight__card__content__news__date">
                        {{ highlightData.news.date ?? '' }}
                    </p>
                </div>
            </div>
        </div>
        <i class="highlight__theme-icon material-symbols-outlined">
            <span style="color: #f4cc01"
            v-if="highlightData.theme === 'space'">
                star
            </span>
            <span style="color: #ccba93"
            v-else-if="highlightData.theme === 'dinosaur'">
                skull
            </span>
            <span style="color: #1d548b"
            v-else-if="highlightData.theme === 'wildlife/ocean'">
                waves
            </span>
        </i>
    </div>
</template>

<script>

export default {
    name: 'MuseumHighlight',
    components: {

    },
    mixins: [
    ],
    props: {
        type: String,
        highlightData: Object,

        /* For random image */
        imageNum: Number,
    },
    data() {
        return {

        };
    },
    computed: {

    },
    methods: {

    },
    created() {

    },
};
</script>

<style lang="scss" scoped>
.highlight {
    width: 100%;
    position: relative;
    &__theme-icon {
        position: absolute;
        top: -18px;
        right: -18px;
        font-size: 36px;
        text-shadow: 2px 3px 5px rgba(50, 50, 93, 0.25);
    }
    &__card {
        display: flex;
        flex-direction: column;
        height: 100%;
        box-shadow: rgba(50, 50, 93, 0.15) 0px 13px 27px -5px, rgba(0, 0, 0, 0.2) 0px 8px 16px -8px;
        /* border: solid #ccc 1px; */
        border-radius: 16px;
        overflow: hidden;
        &__banner {
            width: 100%;
            height: 192px;
            position: relative;
            display: flex;
            align-items: flex-end;
            object-fit: none;
            &__image {
                position: absolute;
                width: 100%;
                height: 100%;
                object-fit: cover;
            }
            &__shadow {
                position: absolute;
                width: 100%;
                height: 100%;
                background:
                    linear-gradient(90deg, #000000 0%, rgba(0, 0, 0, 0) 50%),
                    linear-gradient(0deg, #000000 0%, rgba(0, 0, 0, 0) 50%);
            }
            &__title {
                position: absolute;
                bottom: 0;
                padding-left: 0.5rem;
                padding-right: 0.5rem;
                padding-bottom: 0.25rem;
                color: #fff;
                font-size: 20px;
                font-weight: 300;
                margin: 0em;
            }
        }
        &__content {
            flex: 1 1 0%;
            display: flex;
            flex-direction: column;
            padding: 0.5rem;
            gap: 0.5rem;
            &__details {
                height: 2rem;
                display: flex;
                justify-content: space-between;
                &__date {
                    font-size: 14px;
                }
                &__quiz {
                    height: fit-content;
                    display: flex;
                    align-items: center;
                    gap: 0.5rem;
                    a, i {
                        color: #00f;
                        font-size: 14px;
                    }
                    a {
                        text-decoration: none;
                    }
                    a:hover {
                        text-decoration: underline;
                    }
                }
                &__period {
                    font-size: 14px;
                    font-weight: 600;
                    color: #0a0
                }
                &__habitat {
                    display: flex;
                    flex-direction: column;
                    align-items: flex-end;
                    &__species {
                        font-size: 14px;
                        font-weight: 600;
                        color: #00a
                    }
                    &__location {
                        font-size: 12px;
                        font-style: italic;
                    }
                }
            }
            &__description {
                flex: 1 1 0%;
                p {
                    font-size: 12px;
                }
            }
            &__divider {
                margin-left: 1rem;
                margin-right: 1rem;
                border-top: solid 1px #eee;
            }
            &__news {
                display: flex;
                &__title {
                    font-size: 12px;
                    font-style: italic;
                }
                &__date {
                    font-size: 12px;
                }
            }
        }
        &__info {
            color: #242424;
            font-size: 12px;
            font-weight: 400;
            margin: 0em;
        }
    }
}
.dark-theme {
    background: #242424;
    color: #fff;
}
</style>
