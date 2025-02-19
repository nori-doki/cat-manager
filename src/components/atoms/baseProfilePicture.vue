<template>
    <div class="base-profile-picture">
        <div class="base-profile-picture-frame" :style="{ borderColor: frameColor,
            filter: props.deceased && !props.adopted ? 'grayscale(100%)' : 'none'
         }">
            <img :src="profilePicture" alt="cat profile picture"
            >
        </div>
        <div class="base-profile-picture-name" :style="{ backgroundColor: frameColor }">
            {{ name }}
        </div>
        <div class="base-profile-picture-age" :style="{ backgroundColor: frameColor }">
            {{ getAge() + '🕯️'}} 
        </div>
        <div v-if="gender && gender === 'female'" class="base-profile-picture-gender" :style="{ borderColor: frameColor }"> 
            <i class="pi pi-venus female"></i>
        </div>
        <div v-if="gender && gender === 'male'" class="base-profile-picture-gender" :style="{ borderColor: frameColor }"> 
            <i class="pi pi-mars male"></i>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
    profilePicture: String,
    name: String,
    gender: String,
    socialized: Boolean,
    adoptable: Boolean,
    adopted: Boolean,
    deceased: Boolean,
    dateOfBirth: String,
    dateOfRescue: String
});

const frameColor = computed(() => {
    if (props.adopted) {
        // blue
        return 'rgb(63, 127, 255)';
    } else if (props.deceased && !props.adopted) {
        // black
        return 'rgb(92, 92, 92)';
    } else if (!props.adoptable) {
        // pinkish red
        return 'rgb(238, 29, 102)';
    } else {
        // green
        return 'rgb(118, 195, 136)';
    }
});

const isAdoptable = computed(() => {
    return props.adoptable && !props.adopted && !props.deceased;
});

function getAge() {
    const dateOfBirth = new Date(props.dateOfBirth);
    const today = new Date();
    const diffTime = Math.abs(today - dateOfBirth);
    const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24 * 365));
    // return diffDays + ` ${diffDays > 1 ? 'ans' : 'an'}`;
    return diffDays;
}

function getDaysPassedSinceRescue() {
    const dateOfdateOfRescue = new Date(props.dateOfRescue);
    const today = new Date();
    const diffTime = Math.abs(today - dateOfdateOfRescue);
    const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
    return diffDays;
}
</script>

<style lang="scss">
.base-profile-picture {
    width: fit-content;
    padding: 0 15px;
    display: flex;
    flex-direction: column;
    align-items: center;

    &-frame {
        display: inline-block;
        width: 100px;
        height: 100px;
        border-radius: 50%;
        border: 8px solid rgb(118, 195, 136);
        position: relative;
        overflow: hidden;
        background-color: rgb(92, 92, 92);
        text-align: center;
    }
    img {
        width: auto;
        height: 100%;
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
    }
    &-name {
        z-index: 1;
        margin-top: -5px;
        color: white;
        width: fit-content;
        padding: 5px 10px 5px;
        border-radius: 1rem;
        font-weight: 700;
        font-size: 1.2rem;
    }
    &-age {
        z-index: 1;
        color: white;
        width: fit-content;
        padding: 11px 5px;
        border-radius: 1.7rem;
        position: relative;
        top: -140px;
        left: -50px;
        font-size: 0.85rem;
    }
    &-gender {
        z-index:1;
        background-color: white;
        width: fit-content;
        padding: 5px 7px;
        border-radius: 1.5rem;
        border: 5px solid rgb(63, 127, 255);
        scale: 0.9;
        position: relative;
        top: -175px;
        right: -50px;
        .female {
            color: rgb(255, 115, 248);
        }
    
        .male {
            color: rgb(54, 88, 255);
        }
    }
    &-rescue-countdown {
        z-index: 1;
        color: white;
        width: fit-content;
        padding: 7px 9px;
        border-radius: 1.7rem;
        position: relative;
        top: -145px;
        right: -60px;
    }

}
</style>