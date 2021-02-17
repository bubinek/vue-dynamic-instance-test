<template>
    <div>
        <button @click="createInstance">
            Create Instance
        </button>

        <button @click="callRef">
            Call ref on 1st instance
        </button>

        <div v-for="dialog in instances">
            <Dialog :key="dialog.id" :ref="`dialog-${dialog.id}`" :data="dialog" @close="destroyInstance" />
        </div>
    </div>
</template>

<script>
    import {v4 as uuidv4} from 'uuid'
    import Dialog from './Dialog'

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
                const components = ['TypeA', 'TypeB', 'TypeC']

                this.instances.push({
                    id: uuidv4(),
                    x: Math.floor(Math.random() * 10),
                    y: Math.floor(Math.random() * 10),
                    component: components[Math.floor(Math.random() * components.length)],
                })
            },

            destroyInstance(instance) {
                this.instances.splice(this.instances.findIndex(dialog => dialog.id === instance.id), 1)
            },

            callRef() {
                if (this.instances.length < 1) {
                    return
                }

                console.log(this.$refs[`dialog-${this.instances[0].id}`][0].getDialogData())
            },
        },
    }
</script>
