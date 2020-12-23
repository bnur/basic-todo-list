<template>
    <div class="row container d-flex justify-content-center">
        <div class="card px-3 mt-5 w-100">
          <div class="card-body">
            <h4 class="card-title">My Todo List</h4>
            <div class="add-items d-flex">
              <input
                type="text"
                class="form-control todo-list-input"
                placeholder="What will i do today?"
                v-model="todoContent"
              />
              <button class="add btn btn-primary font-weight-bold todo-list-add-btn" @click="AddTodo">Add</button>
            </div>
  
            <div class="list-wrapper">
              <ul class="d-flex flex-column-reverse todo-list">
                <li v-for="todo in todoList">
                  <div class="form-check">
                    <label class="form-check-label  mt-1">
                      <input class="checkbox" type="checkbox" :checked="todo.status == 1" @click="UpdateStatus($event,todo.id)"/>
                      {{todo.content}}
                      <button type="button" class="btn btn-outline-primary btn-sm" @click="DeleteRecord($event,todo.id)">Delete</button>
                    </label>
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
    export default{
        data(){
            return{
              todoContent:"",
              todoList:[
                  {
                    id:0,
                    content:"Read book",
                    status:1
                  },
                  {
                    id:1,
                    content:"Research anything",
                    status:0
                  }
                ]
            }
        },
        methods:{
          UpdateStatus(event,id){
            var todo=this.todoList.find(x=>x.id==id);
            todo.status==0 ? todo.status=1 : todo.status=0
          },
          DeleteRecord(event,id){
            confirm('Are you sure you want to delete this todo?') ? this.todoList.pop(x=>x.id==id) : console.log("Error");
          },

          AddTodo(){
            console.log(this.todoContent);
            var newTodo={
              id:this.todoList.length,
              content:this.todoContent,
              status:0
            }
            this.todoList.push(newTodo);
          }
        },
        created(){
            console.log(this.todoList);

        }
    }
    
</script>


<style>
</style>