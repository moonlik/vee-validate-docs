<template>
    <div class="note">
        <b>{{ capitalize(title) }}:</b> <slot></slot>
    </div>
</template>

<script>
export default {
    name: 'note',
    props: {
        title: {
            type: String,
            default: 'Note'
        },
        type: {
            type: String,
            default: 'info'
        }
    },
    methods: {
        capitalize(str) {
            return str.charAt(0).toUpperCase() + str.slice(1);
        }
    }
};
</script>
