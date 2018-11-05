<template>
    <Page class="page">
        <ActionBar class="action-bar">
            <Label class="action-bar-title" text="Todos Demo"></Label>
        </ActionBar>

        <StackLayout>
            <Label textWrap='true' col='0' row='1'> {{todos}} </Label>

            <!-- GRIDLAYOUT FOR INPUT AND BUTTON -->
            <GridLayout columns='*,*,*,*,*,*' rows='*' height='40'>
                <TextField v-model='input' col='0' row='0' hint="Enter Something" />
                <Button @tap='addTodo(input)' col='1' row='0' text="ADD" />

                <Button @tap='i--' col='2' row='0' text="-" />
                <TextField v-model='i' col='3' row='0' hint="Enter Index" />
                <Button @tap='i++' col='4' row='0' text="+" />
                <Button @tap='deleteTodo(i)' col='5' row='0' text="DELETE" />
            </GridLayout>

            <Label textWrap='true'>You are deleting: {{todos[i]}} </Label>

        </StackLayout>

    </Page>
</template>

<script>
    export default {

        data() {
            return {
                todos: [],
                input: "",
                i: 0,
            }
        },

        methods: {

            addTodo(todo) {
                this.todos.push(todo)
                this.input = ""
            },

            deleteTodo(i) {
                this.todos.splice(i, 1)
            }

        },

        computed: {
            message() {
                return "Blank {N}-Vue app";
            }
        }
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
</style>