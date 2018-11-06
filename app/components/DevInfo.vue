<template>
    <Page class="page">
        <ActionBar class="action-bar" title='Dev Page'></ActionBar>

        <StackLayout>

            <Label textWrap='true' :text='todos' />
            
        </StackLayout>

    </Page>
</template>

<script>

let date = require('date-and-time');

    export default {

        props: ['tododata'],
        
        data() {
            return {
                todos: this.tododata,
            }
        },

        methods: {

        },

    };
</script>

<style scoped lang="scss">
    // Start custom common variables
    @import '../app-variables';
    // End custom common variables

    // Custom styles
    .fa {
        color: $accent-dark;
    }

    .info {
        font-size: 20;
    }

    .done {
        text-decoration: line-through;
    }
</style>