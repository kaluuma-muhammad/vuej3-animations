<template>
    <div class="home">
        <transition name="toast">
            <Toast v-if="showToast" />
        </transition>
        <Todos @badValue="triggerToast" />
    </div>
</template>

<script>
    import Toast from '../components/Toast.vue'
    import Todos from '../components/Todos.vue'
    import { ref } from 'vue'

    export default {
        name: 'Home',
        components: { Toast, Todos },
        setup() {
            const showToast = ref(false)

            const triggerToast = () => {
                showToast.value = true
                setTimeout(() => showToast.value = false, 3000)
            }

            return { showToast, triggerToast }
        }
    }
</script>

<style>
    .toast-enter-active {
        animation: wobble 0.5s ease;
    }
    .toast-leave-from {
        opacity: 1;
        transform: translateY(0);
    }
    .toast-leave-to {
        opacity: 0;
        transform: translateY(-60px);
    }
    .toast-leave-active {
        transition: all 0.3s ease;
    }

    @keyframes wobble {
        0% { transform: translateY(-60px); opacity: 0; }
        50% { transform: translateY(0px); opacity: 1; }
        60% { transform: translateX(8px) }
        70% { transform: translateX(-8px) }
        80% { transform: translateX(4px) }
        90% { transform: translateX(-4px) }
        100% { transform: translateX(0) }
    }
</style>
