<template>
    <div class="dialog">
        <div>
            I'm single instance of Dialog.vue.
        </div>

        <div>
            Props:

            {{ data }}
        </div>

        <div>
            <component :is="dynamicComponent" />
        </div>

        <div>
            <button @click="$emit('close', data)">
                Destroy instance
            </button>
        </div>
    </div>
</template>

<script>
    const TypeA = () => import('./widgets/TypeA')
    const TypeB = () => import('./widgets/TypeB')
    const TypeC = () => import('./widgets/TypeC')

    export default {
        props: {
            data: {
                type: Object,
                required: true,
            },
        },

        computed: {
            dynamicComponent() {
                switch (this.data.component) {
                    case 'TypeA':
                        return TypeA

                    case 'TypeB':
                        return TypeB

                    case 'TypeC':
                        return TypeC

                    default:
                        throw new Error(`Unknown component type: "${this.data.component}"`)
                }
            },
        },
    }
</script>

<style>
    .dialog {
        border: 1px dashed #336688;
        margin: 16px;
        padding: 0 16px;
    }

    .dialog > div {
        margin: 16px 0;
    }
</style>
