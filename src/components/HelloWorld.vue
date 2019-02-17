<template>
  <div class="todos">
    <div class="col-md-4">
      <h1>Pending</h1>
      <button @click="getTodos">Get Tasks</button>
      <ol>
        <draggable v-model="pending" @start="isDragging=true" @end="isDragging=false">
          <transition-group>
            <li class="todo" v-for="todo in pending" :key="todo._id">
              {{ todo.name }}
            </li>
          </transition-group>
        </draggable>
      </ol>
    </div>
    <div class="col-md-4">
      <h1>On Going</h1>
      <ol>
        <draggable v-model="onGoing">
          <transition-group>
          <li class="todo" v-for="todo in onGoing" :key="todo._id">
            {{ todo.name }}
          </li>
          </transition-group>
        </draggable>
      </ol>
    </div>
    <div class="col-md-4">
      <h1>Completed</h1>
      <ol>
        <draggable v-model="completed">
          <transition-group>
            <li class="todo" v-for="todo in completed" :key="todo._id">
              {{ todo.name }}
            </li>
          </transition-group>
        </draggable>
      </ol>
    </div>
  </div>
</template>

<script>
  import {HTTP} from '../http-constants';
  import draggable from 'vuedraggable';

  export default {
    components: {
      draggable
    },
    name: 'HelloWorld',
    props: {
      msg: String
    },
    data () {
      return {
        pending: [],
        onGoing: [],
        completed: [],
        errors: ''
      }
    },
    methods: {
      getTodos: function () {
        HTTP.get('/tasks')
                .then(response => {
                  this.pending = response.data;
                })
                .catch(e => {
                  this.errors = e;
                })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
  .todo{
    height: 100px;
    width: 100px;
    border-color: yellow;
    background-color: lightgoldenrodyellow;
    border-style: solid;
    border-width: thin;
    text-align: center;
    padding-top:50px;
  }

</style>
