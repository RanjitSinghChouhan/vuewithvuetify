<template>
  <div>
    <br />
    <br />
    <div v-if="!editing">
      <form @submit.prevent="onSubmit" class="todo-input">
        <input type="text" v-model="title" :id="id" />
        <input type="submit" value="Add Todo" />
      </form>
    </div>
    <div v-else>
      <form @submit.prevent="updateTodo" class="todo-input">
        <input type="text" v-model="editedTitle" :id="editedId" />
        <input type="submit" value="Update" />
      </form>
    </div>

    <br />
    <br />
    <!-- <button @click="fetchTodos">Fetch Here</button> -->
    <!-- <div class="todos">
      <div v-for="todo in todos" :key="todo.id" :todo="todo">
        {{ todo.title }}
      </div>
    </div> -->
    <v-layout
      class="d-flex align-content-start flex-wrap"
      color="grey lighten-2"
      flat
      tile
      max-height="200"
      max-width="100"
    >
      <v-flex
        class="pa-2"
        outlined
        tile
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
      >
        <!-- <v-card class="mx-auto ma6" max-width="344" outlined>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-4">{{ todo.id }}</div>
              <v-list-item-title class="text-h5 mb-1">
                {{ todo.completed }}
              </v-list-item-title>
              <v-list-item-subtitle>{{ todo.title }}</v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-avatar
              tile
              size="80"
              color="grey"
            ></v-list-item-avatar> -->

        <!-- new card -->

        <v-card class="mx-auto" max-width="344" variant="outlined">
        
          <v-card-header>
            <div>
              <div class="text-overline mb-1">
                {{ todo.id }}
              </div>
              <div class="text-h6 mb-1">
                {{ todo.completed }}
              </div>
              <div class="text-caption">{{ todo.title }}</div>
            </div>
          </v-card-header>

          <v-card-actions>
            <v-btn
              variant="outlined"
              rounded
              text
              color="red"
              @click="removeTodo(todo)"
            >
              Delete
            </v-btn>
            <v-btn
              variant="outlined"
              rounded
              text
              color="green"
              @click="editTodo(todo.title, todo.id, todo.completed)"
              :key="todo.id"
            >
              Edit
            </v-btn>
          </v-card-actions>
        </v-card>

        <!-- </v-list-item>

          <v-card-actions>
            <v-btn outlined rounded text color="red" @click="removeTodo(todo)">
              Delete
            </v-btn>
            <v-btn outlined rounded text color="green" @click="editTodo(todo)">
              Edit Todo
            </v-btn>
          </v-card-actions>
        </v-card> -->
      </v-flex>
    </v-layout>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import store from "../store";

@Options({})
export default class Fetch extends Vue {
  public title = "";
  public id = 0;
  completed = true;
  editing = false;
  editedTitle = "";
  editedId = 0;
  editedCompleted = true;

  public addTodo(title: string): void {
    store.dispatch("addTodo", title);
    this.title = "";
  }
  onSubmit() {
    this.addTodo(this.title);
  }

  public removeTodo(todo: string): void {
    store.dispatch("removeTodo", todo);
  }

  editTodo(title: string, id: number, completed: boolean): void {
    this.editedId = id;
    this.editing = true;
    this.editedTitle = title;
    this.editedCompleted = completed;
    console.log(this.editedTitle, this.id, this.editedCompleted);
  }

  updateTodo(): void {
    let payload = {
      title: this.editedTitle,
      id: this.editedId,
      completed: this.editedCompleted,
    };
    store.dispatch("updateTodo", payload);
    this.editedTitle = "";
    this.editing = false;
  }

  get todos() {
    return store.state.todos;
  }

  mounted() {
    store.dispatch("fetchTodos");
  }

  //   created() {
  //     this.fetchTodos;
  //   }
}
</script>


<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 10px;
  border: 1px solid #41b883;
  outline: 0;
}
input[type="submit"] {
  flex: 2;
  background: #41b883;
  color: #fff;
  border: 1px #41b883 solid;
  cursor: pointer;
}
</style>
