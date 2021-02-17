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
            <button @click="$emit('close', data)">
                Destroy instance
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            data: {
                type: Object,
                required: true,
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
