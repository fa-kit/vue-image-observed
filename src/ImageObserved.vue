<template>
    <img 
        :src="src" 
        :alt="alt"
        :class="imageClass"
        v-if="isVisible">
    <Placeholder
        :padding-bottom="ratioPercent"
        :class="imageClass"
        v-else/>
</template>

<script>
import Placeholder from '@fakit/vue-placeholder'
export default {
    props: {
        src: String,
        alt: String,
        imageClass: String,
        observerMargin: {
            type: String,
            default: '100px 0px 100px 0px'
        },
        ratioPercent: {
            type: String,
            default: '60%'
        }
    },
    data(){
        return {
            observerOptions: {
                rootMargin: this.observerMargin,
                threshold: 0
            },
            observer: null,
            isVisible: false
        }
    },
    components: {
        Placeholder,
    },
    mounted(){
        this.observer = new IntersectionObserver(this.observeImage, this.observerOptions);
        this.observer.observe(this.$el);
    },
    computed: {},
    methods: {
        observeImage(entries, observer){
            if(entries[0].isIntersecting){
                this.isVisible = true;
                this.observer.disconnect();
            }
        }
    }
}
</script>