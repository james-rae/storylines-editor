<template>
    <div class="relative">
        <div class="absolute top-0 right-0 bg-white text-black p-2">
            {{ $t('editor.landing.greeting') }} {{ userName }}!
        </div>
        <div class="flex flex-col items-center">
            <h1 class="text-2xl font-bold mt-4">{{ title }}</h1>
            <div class="flex justify-center mt-12 mb-32">
                <div class="lang-selector border-4 border-gray-400 border-solid mx-8">
                    <router-link
                        :to="{ name: 'home', params: { lang: 'en' } }"
                        class="flex justify-center h-full w-full"
                        target
                    >
                        <button class="text-2xl text-white font-bold">English</button>
                    </router-link>
                </div>
                <div class="lang-selector border-4 border-gray-400 border-solid mx-8">
                    <router-link
                        :to="{ name: 'home', params: { lang: 'fr' } }"
                        class="flex justify-center h-full w-full"
                        target
                    >
                        <button class="text-2xl text-white font-bold">Français</button>
                    </router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Vue } from 'vue-property-decorator';
import { useUserStore } from '../stores/userStore';

export default class LandingV extends Vue {
    title = document.title;
    url = window.location.href;

    beforeCreate(): void {
        // Automatically choose lang and re-route when the user is using Canada.ca template
        if (this.url.includes('index-ca')) {
            const lang = this.url.includes('index-ca-en') ? 'en' : 'fr';
            this.$router.push({
                name: 'home',
                params: { lang }
            });
        }
    }

    get userName(): string {
        const userStore = useUserStore();
        return userStore.userProfile?.userName || 'Guest';
    }
}
</script>

<style lang="scss">
.lang-selector {
    height: 18vh;
    width: 32vh;
    background-color: #26374a;
}
.lang-selector:hover {
    background-color: #2572b4;
}
</style>
