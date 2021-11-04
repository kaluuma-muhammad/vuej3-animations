<template>
    <div class="about">
        <transition appear @before-enter="beforeEnter" @enter="enter">
            <h1> About </h1>
        </transition>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
    </div>
</template>

<script>
    import { ref } from 'vue'
    import gsap from 'gsap'

    export default {
        name: 'About',
        setup() {
            const beforeEnter = (el) => {
                el.style.transform = 'translateY(-60px)'
                el.style.opacity = 0
            }
            const enter = (el, done) => {
                gsap.to(el, {
                    duration: 1, y: 0, opacity: 1, ease: 'bounce.out', onComplete: done
                })
            }

            return { beforeEnter, enter }
        }
    }
</script>

<style>
    .about {
        max-width: 600px;
        margin: 20px auto;
    }
</style>
