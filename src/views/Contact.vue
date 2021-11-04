<template>
    <div class="contact">
        <transition appear @before-enter="beforeTitleEnter" @enter="enterTitle">
            <h1> Contact </h1>
        </transition>
        <transition-group tag="ul" appear @before-enter="beforeEnter" @enter="enter">
            <li v-for="(icon, index) in icons" :key="icon.name" :data-index="index">
                <span class="material-icons">{{ icon.name }}</span>
                <div>{{ icon.text }}</div>
            </li>
        </transition-group>
    </div>
</template>

<script>
    import { ref } from 'vue'
    import gsap from 'gsap'

    export default {
        name: 'Contact',
        setup () {
            const icons = ref([
                { name: 'alternate_email', text: 'by email'},
                { name: 'local_phone', text: 'by phone'},
                { name: 'local_post_office', text: 'by post'},
                { name: 'local_fire_department', text: 'by smoke signal'}
            ])
            const beforeEnter = (el) => {
                el.style.transform = 'translateY(100px)'
                el.style.opacity = 0
            }
            const enter = (el, done) => {
                gsap.to(el, {
                    duration: 0.8, y: 0, opacity: 1, onComplete: done, delay: el.dataset.index * 0.2
                })
            }
            const beforeTitleEnter = (el) => {
                el.style.transform = 'translateY(-60px)'
                el.style.opacity = 0
            }
            const enterTitle = (el, done) => {
                gsap.to(el, {
                    duration: 1, y: 0, opacity: 1, ease: 'bounce.out', onComplete: done
                })
            }

            return { icons, beforeEnter, enter, beforeTitleEnter, enterTitle };
        }
    }
</script>

<style>
    .contact ul {
        padding: 0;
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
        max-width: 400px;
        margin: 60px auto;
    }

    .contact li {
        list-style-type: none;
        background: white;
        padding: 30px;
        border-radius: 10px;
        box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
        cursor: pointer;
        line-height: 1.5em;
    }
</style>
