<template>
    <div class="space-page">
        <div class="space-page__head responsive-container">
            <h2 class="space-page__head__title">
                Space
            </h2>
            <div class="space-page__head__pagination">
                <button @click="() => changePage(-1)"
                class="space-page__head__pagination__button">
                    <i class="material-symbols-outlined">chevron_left</i>
                </button>
                <p class="space-page__head__pagination__number">
                    {{ pageNumber + 1 }}
                </p>
                <button @click="() => changePage(1)"
                class="space-page__head__pagination__button">
                    <i class="material-symbols-outlined">chevron_right</i>
                </button>
            </div>
        </div>
        <div class="space-page__content">
            <div class="space-page__content__cards responsive-container"
            :v-if="highlights">
                <MuseumHighlight
                v-for="(highlight, i) in highlights" :key="i"
                :highlightData="highlight"
                :imageNum="i" />
            </div>
        </div>
    </div>
</template>

<script>

import MuseumHighlight from './MuseumHighlight';

export default {
    name: 'SpacePage',
    components: {
        MuseumHighlight,
    },
    mixins: [
    ],
    props: {

    },
    data() {
        return {
            spaceHighlights: [
                {
                    date: '2020-04-20 12:20:00',
                    description: 'Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.',
                    id: 1,
                    image: '',
                    name: 'Asteroids',
                },
                {
                    date: '2020-05-20 15:50:00',
                    description: 'A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.',
                    id: 9,
                    image: '',
                    name: 'Comets',
                },
                {
                    date: '2020-05-01 9:22:00',
                    description: 'The term planet is ancient, with ties to history, astrology, science, mythology, and religion.',
                    id: 7,
                    image: '',
                    name: 'Planets',
                    news: {
                        date: '2020-08-18 18:00:00',
                        title: 'Attend our talk about Jupiter with Dr. Hogarth',
                    },
                    quiz: 'https://planetquiz.space',
                },
                {
                    date: '2020-07-05 4:10:00',
                    description: 'A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.',
                    id: 12,
                    image: '',
                    name: 'Meteor showers',
                    news: {
                        title: 'The Lyrids will peak at on April 21-22 2021, at night',
                    },
                },
            ],
            spacePartners: {
                observatory: {
                    createdAt: '2020-06-01 11:45:00',
                    info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
                    image: '',
                    name: 'Mauna Kea Observatories',
                },
            },
            apiData: [],
            pageNumber: 0,
            highlightsPerPage: 12,
        };
    },
    computed: {
        highlights() {
            let vm = this;
            return vm.apiData.slice(
                vm.pageNumber * vm.highlightsPerPage,
                (vm.pageNumber + 1) * vm.highlightsPerPage
            );
        }
    },
    methods: {
        changePage(val) {
            let vm = this;
            vm.pageNumber += val;
            if (vm.pageNumber < 0) {
                vm.pageNumber = 0;
            }
            else if(vm.pageNumber > vm.apiData.length / vm.highlightsPerPage) {
                vm.pageNumber = Math.floor(vm.apiData.length / vm.highlightsPerPage);
            }
        },
        formatData(data) {
            let result = data;
            if (result.createdAt || result.date) {
                result.date = new Date(result.createdAt ?? result.date);
            }
            if (result.news?.date) {
                result.news.date = new Date(result.news.date);
            }
            result.description = result.info ?? result.description;
            return result;
        }
    },
    created() {
        let vm = this;
        vm.spaceHighlights.forEach(highlight => {
            highlight.theme = 'space';
            highlight.partner = false;
            vm.apiData.push(vm.formatData(highlight))
        });
        Object.values(vm.spacePartners).forEach(highlight => {
            highlight.theme = 'space';
            highlight.partner = true;
            vm.apiData.push(vm.formatData(highlight))
        });
        vm.apiData.sort((a,b) => Number(b.date) - Number(a.date));
        vm.apiData.map(highlight => {
            let result = highlight;
            if (result.date) {
                result.date = result.date.toLocaleDateString('en-GB', { timeZone: 'GMT' });
            }
            if (result.news?.date) {
                result.news.date = result.news.date.toLocaleDateString('en-GB', { timeZone: 'GMT' });
            }
            return result;
        });
    },
};
</script>

<style lang="scss" scoped>
.space-page {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    &__head {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
        &__title {
            margin: 0;
            color: #242424;
            font-size: 32px;
            font-weight: 300;
            letter-spacing: 0.05rem;
        }
        &__pagination {
            display: flex;
            justify-content: center;
            align-items: flex-end;
            gap: 0.5rem;
            &__button {
                cursor: pointer;
                height: fit-content;
                background: none;
                border: none;
                color: #242424;
                i {
                    font-size: 20px;
                }
            }
            &__number {
                margin: 0;
                font-size: 20px;
                font-weight: 300;
                color: #242424;
            }
        }
    }
    &__content {
        position: relative;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        overflow-x: hidden;
        overflow-y: auto;
        scrollbar-gutter: stable both-edges;
        &__cards {
            display: grid;
            grid-template-columns: repeat(1, minmax(0, 1fr));
            @media (min-width: 760px){
                grid-template-columns: repeat(2, minmax(0, 1fr));
            }
            @media (min-width: 1024px){
                grid-template-columns: repeat(3, minmax(0, 1fr));
            }
            padding-top: 2rem;
            padding-bottom: 2rem;
            row-gap: 3rem;
            column-gap: 2rem;
            position: absolute;
            top: 0px;
        }
    }
}
</style>
