<template>
    <div>
        <button @click="createInstance">
            Create Instance
        </button>

        <div v-for="dialog in instances">
            <Dialog :key="dialog.id" :data="dialog" @close="destroyInstance" />
        </div>
    </div>
</template>

<script>
    import {v4 as uuidv4} from 'uuid'
    import Dialog from './Dialog.vue'

    export default {
        components: {
            Dialog,
        },

        data() {
            return {
                instances: [],
            }
        },

        methods: {
            createInstance() {
                this.instances.push({
                    id: uuidv4(),
                    x: Math.floor(Math.random() * 10),
                    y: Math.floor(Math.random() * 10),
                })
            },

            destroyInstance(instance) {
                this.instances.splice(this.instances.find(dialog => dialog.id === instance.id), 1)
            },
        },
    }
</script>
