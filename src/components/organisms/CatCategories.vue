<template>
    <div class="cat-categories">
        <h2>{{ numberOfCats }} chats pris en charge depuis la création de l'association en décembre 2024 🎉</h2>
        <div v-for="category in categories " class="category" :key="category.id">
            <div style="display: flex; flex-direction: row;">
                <div style="width: 100%;">
                    <h3 class="category-title" >{{ `${catList.filter(category.filter).length} ${category.label}` }}</h3>
                </div>
                <div style="padding: 5px; margin: 5px; width: fit-content; cursor: pointer;"
                @click="category.show = !category.show"
                >
                    <i v-if="!category.show" class="pi pi-angle-up"></i>
                    <i v-else class="pi pi-angle-down"></i>
                </div>
            </div>
            <div v-show="category.show" class="category-container">
                <baseProfilePicture 
                    v-for="cat in catList.filter(category.filter)"
                    :profilePicture="cat.profile_picture"
                    :name="cat.name"
                    :key="cat.id"
                    :gender="cat.gender"
                    :socialized="cat.socialized"
                    :adoptable="cat.adoptable"
                    :adopted="cat.adopted"
                    :deceased="cat.date_of_decease !== null"
                    :date-of-birth="cat.date_of_birth"
                    :date-of-rescue="cat.date_of_rescue"
                    />
            </div>
        </div>
    </div>
</template>

<script setup>
import baseProfilePicture from '../atoms/baseProfilePicture.vue';
import { computed, ref } from 'vue';

const catList = [
    {
        id: 1,
        created_at: '2025-02-01',
        name: 'Tichoco',
        date_of_birth: '2022-01-01',
        zip_code: '75013',
        profile_picture: 'https://mypetsays.co.uk/cdn/shop/articles/National_Black_Cat_Day.jpg?v=1695635944&width=600',
        adoptable: false,
        socialized: false,
        foster_name: 'Inès',
        description: 'Tichoco est craintive, elle aime jouer mais garde ses distances et éviter tout contact physique. Elle n\hésite pas à donner un coup de patte si on tente de la toucher.',
        adopted : false,
        date_of_rescue: '2023-01-01',
        gender: 'female',
        date_of_decease: null
    },
    {
        id: 6,
        created_at: '2025-02-01',
        name: 'Chanwar',
        date_of_birth: '2022-01-01',
        zip_code: '75013',
        profile_picture: 'https://mypetsays.co.uk/cdn/shop/articles/National_Black_Cat_Day.jpg?v=1695635944&width=600',
        adoptable: true,
        socialized: false,
        foster_name: 'Inès',
        description: 'Tichoco est craintive, elle aime jouer mais garde ses distances et éviter tout contact physique. Elle n\hésite pas à donner un coup de patte si on tente de la toucher.',
        adopted : false,
        date_of_rescue: '2023-01-01',
        gender: 'male',
        date_of_decease: null
    },
    {
        id: 2,
        created_at: '2025-02-01',
        name: 'Florine',
        date_of_birth: '2009-12-01',
        zip_code: '75013',
        profile_picture: 'https://cdn.mos.cms.futurecdn.net/iVqE9GQDEA5LeNYsvM5g2C-650-80.png.webp',
        adoptable: true,
        socialized: true,
        foster_name: 'Inès',
        description: 'Florine est sociable et caline, elle aime jouer et les moments de tendresse.',
        adopted : false,
        date_of_rescue: '2024-11-27',
        gender: 'female',
        date_of_decease: null
    },
    {
        id: 3,
        created_at: '2025-02-01',
        name: 'Nori',
        date_of_birth: '2015-10-01',
        zip_code: '75012',
        profile_picture: 'https://www.catster.com/wp-content/uploads/2023/11/tuxedo-cat-with-yellow-eyes_Rosalia-Ricotta_Pixabay.jpg.webp',
        adoptable: true,
        socialized: true,
        foster_name: 'Inès',
        description: 'Nori est un chat très sociable, il aime jouer et chasser. Il est très proche de l\'homme.',
        adopted : true,
        gender: 'male',
        date_of_rescue: '2015-11-26',
        date_of_decease: null
    },
    {
        id: 4,
        created_at: '2025-02-01',
        name: 'Momo',
        date_of_birth: '2016-06-15',
        zip_code: '75014',
        profile_picture: 'https://static.vecteezy.com/ti/photos-gratuite/p2/6240415-chat-tigre-gris-argente-photo.jpg',
        adoptable: true,
        socialized: true,
        foster_name: 'Inès',
        description: 'Momo est un chat très sociable, il aime jouer et être caressé. Il est très proche de l\'homme. Il s\'est fait renversé par une voiture le 18/02/2021.',
        adopted : true,
        gender: 'male',
        date_of_rescue: '2016-09-15',
        date_of_decease: '2021-02-18'
    },
    {
        id: 5,
        created_at: '2025-02-01',
        name: 'Malo',
        date_of_birth: '2024-06-15',
        zip_code: '75014',
        profile_picture: 'https://img.kleinezeitung.at/public/incoming/6l40qc-HANDOUT-WEITERE-KATZE-MACHT-BEI-POLIZEI-REITERSTAFFEL-DIENST-GESCHWISTERCHEN-FR-MIETZE-LEUTNANT_1558246588927797_v0_l.jpg/alternates/KLZ_SOCIAL/-HANDOUT--WEITERE-KATZE-MACHT-BEI-POLIZEI-REITERSTAFFEL-DIENST---GESCHWISTERCHEN-FR-MIETZE-LEUTNANT_1558246588927797_v0_l.jpg',
        adoptable: true,
        socialized: true,
        foster_name: 'Laure',
        description: 'Momo est un chat très sociable, il aime jouer et être caressé. Il était en FALD au comissariat du 20ème. Décédé le 04/02/2025.',
        adopted : false,
        gender: 'male',
        date_of_rescue: '2024-09-15',
        date_of_decease: '2025-02-04'
    },
];

const categories = ref([
    {
        id: 1,
        label: ' chats à l\'adoption 🏆',
        filter: cat => cat.adoptable && !cat.adopted && cat.date_of_decease === null,
        show: true
    },
    {
        id: 2,
        label: 'chats pas encore adoptables ⏳',
        filter: cat => !cat.adoptable,
        show: false
    },
    {
        id: 3,
        label: 'chats adoptés ❤️',
        filter: cat => cat.adopted,
        show: false
    },
    {
        id: 4,
        label: 'chats partis trop tôt... 🕊️',
        filter: cat => cat.date_of_decease !== null && !cat.adopted,
        show: false
    }
])

const numberOfCats = computed(() => catList.length);

</script>

<style lang="scss">
.cat-categories {

    h2 {
        text-align: center;
        padding: 1rem;
        margin: auto;
        width: 95%;
    }

    .category {
            box-shadow: 3px 3px 10px 1px rgba(0, 0, 0, 0.15);
            border-radius: 1rem;
            margin: 1rem;
            padding: 1rem 0.5rem;
            background-color: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(30px);
            transition: transform 0.9s ease-in-out;

        .category-title {
            padding: 5px;
            margin: 5px;
            text-align: left;
            font-size: 1.2rem;
        }

        .category-container {
            display: flex;
            gap: 10px;
            padding: 10px;
            justify-content: center;
        }

    }
}
</style>