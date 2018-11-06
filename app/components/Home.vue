<template>
    <Page class="page">
        <ActionBar class="action-bar" title='Todos Demo'></ActionBar>

        <StackLayout>
            <!-- GRIDLAYOUT FOR INPUT AND BUTTON -->
            <GridLayout columns='4*,2*' rows='*' height='50'>

                <!-- TODO INPUT -->
                <TextField v-model='input' @returnPress='addTodo(input,todos.length)' col='0' row='0' hint="Enter" />

                <!-- ADD TODO BUTTON -->
                <Button @tap='addTodo(input,todos.length)' col='1' row='0' text="ADD" />
            </GridLayout>

            <!-- DISPLAY EVERYTHING -->
            <GridLayout columns='3*,*' rows='3*,*' height='55' v-for='(item,i) in todos' :key='item'>

                <StackLayout col='0' row='0' rowSpan='2' @tap='toggleDone(i)'>
                    <Label :class="{done: item.isDone}" class="h2" verticalAlignment='center' textWrap='true'>{{item.todo}}</Label>
                    <Label :class="{done: item.isDone}" verticalAlignment='center' textWrap='true'>{{item.timeAdded}} on {{item.dateAdded}}</Label>
                </StackLayout>

                <Button col='1' row='0' rowSpan='2' @tap='deleteTodo(i)' text='REMOVE' />
            </GridLayout>

        </StackLayout>

    </Page>
</template>

<script>
    import DevInfoVue from './DevInfo.vue';
    let date = require('date-and-time');

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

                // CHECK FOR INPUT (DEVPAGE) TO NAVIGATE TO DEVPAGE, IF ITS NOT DEVPAGE, PUSH IT TO THE TODOS ARRAY AND DO THE NORMAL STUFF
                if (todo == 'devpage') {
                    this.navigateToDev()
                } else {
                    if (!this.input == '') {
                        this.todos.push({
                            todo: todo,
                            isDone: false,
                            id: i,
                            dateAdded: date.format(new Date(), 'DD MMM YY'),
                            timeAdded: date.format(new Date(), 'hh:mm A')
                        })
                    }
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
            },

            navigateToDev() {
                this.$navigateTo(DevInfoVue, {
                    props: {
                        tododata: JSON.stringify(this.todos),
                    }
                })
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
        color: $disabled;
    }
</style>