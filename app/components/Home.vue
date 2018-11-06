<template>
    <Page class="page">
        <ActionBar class="action-bar" title='Todos Demo'></ActionBar>

        <StackLayout>

            <Label textWrap='true'>{{todos}}</Label>


            <!-- GRIDLAYOUT FOR INPUT AND BUTTON -->
            <GridLayout columns='4*,*' rows='*' height='40'>
                <TextField v-model='input' col='0' row='0' hint="Enter Something" />
                <Button @tap='addTodo(input,todos.length)' col='1' row='0' text="ADD" />
            </GridLayout>

            <!-- DISPLAY EVERYTHING -->
            <GridLayout columns='4*,*,*' rows='*' height='40' v-for='(item,i) in todos' :key='item'>
                <Label :class="{done: item.isDone}" verticalAlignment='center' col='0' row='0' textWrap='true'>{{item.todo}}</Label>
                <Button col='1' row='0' @tap='deleteTodo(i)' text="R" />
                <Button col='2' row='0' @tap='toggleDone(i)' text="D" />
            </GridLayout>

        </StackLayout>

    </Page>
</template>

<script>

    export default {

        data() {
            return {
                todos: [],
                input: "",
                click: 0,
            }
        },

        methods: {

            addTodo(todo, i) {

                if (!this.input == '') {
                    this.todos.push({
                        todo: todo,
                        isDone: false,
                        id: i
                    })
                }
                this.input = ""
            },

            deleteTodo(i) {
                this.todos.splice(i, 1)
            },

            toggleDone(i) {
                this.click++

                // FIRST CLICK
                if (this.click % 2 == 1) {
                    this.todos[i].isDone = true;
                } else {
                    this.todos[i].isDone = false;
                }
            }

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