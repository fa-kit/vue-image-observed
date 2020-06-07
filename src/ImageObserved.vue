<template>
    <div 
        class="case-card">
        <a :href="project.url ? project.url : ''">
            <Card-Image-Frame 
                class="case-card_image"
                :image="project.cover"
                :alt="project.caption"
                :load-image="isVisible"/>
        </a>
        <span
            class="case-card_date">
            {{ project.created | dateFormat }}</span>
        <h4
            class="case-card_title heading heading__h4">
            <a 
                :href="project.url ? project.url : ''">
                {{ project.caption }}</a>
            </h4>
        <p
            class="case-card_description paragraph">
            {{ project.description }}</p>
    </div>
</template>

<script>
import Placeholder from '@fakit/vue-placeholder'
export default {
    props: {
        src: String,
        observerMargin: {
            type: String,
            default: '100px 0px 100px 0px'
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
        CardImageFrame,
    },
    mounted(){
        this.observer = new IntersectionObserver(this.observeCard, this.observerOptions);
        this.observer.observe(this.$el);
    },
    computed: {},
    methods: {
        loadImage(){
            tis.status = true;
            console.log('1');
        },
        observeCard(entries, observer){
            if(entries[0].isIntersecting){
                this.isVisible = true;
                this.observer.disconnect();
            }
        }
    }
}
</script>