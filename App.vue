<template>
  <div class="container"> 
        <div class="row justify-content-center"> 
            <div class="col-md-8 mt-5">
                <div class="card">
                    <div class="card-header">
                        <h2 class="text-center" > FORM </h2>
                       
                    </div>
                     <div class="card-body"> 
                        <div  class="form-group">
                       İsim-Soyisim <input type="text" size="20" v-model="name" placeholder="İsim Giriniz.." class="form-control"> <br> <br>
                        Şifre:  <input type="password" size="20" v-model="sifre" placeholder="Şifre Giriniz..." class="form-control"> <br> <br>
                         Doğum Tarihi:<input type="date" size="20" v-model="tarih" class="form-control"> <br> <br>
                         Email: <input type="email" size="20" v-model="email" placeholder="Email Giriniz..." class="form-control"> <br> <br>
                         Açık Adresiniz:
                         <textarea rows="5" cols="30" v-model="textl"></textarea> <br> <br>
                        <button v-if="!isEditing" @click="create" class="btn-primary"> GÖNDER </button>     
                        
                        <button v-else @click="updateTodo" class="btn btn-primary"> Update </button>     
                    </div>

                    <div class="card">
                    <div class="card-header">
                        <h3 class="text" > GİRİLENLER </h3>
                    </div>
                    <div class="card-body">
                        <table> 
                             <thead>
                                 <tr>
                        <td>AD &emsp;</td>
                        <td>ŞİFRE &emsp;</td>
                        <td>DOĞUM TARİHİ&emsp;</td>
                        <td>TARİH &emsp;</td>
                        <td>EMAİL &emsp;</td>
                        <td>ADRES &emsp;</td> </tr>  </thead> 
<tbody>
                         <tr :key="todo.id" v-for="todo in todos" >  
                          
                     
                        <td>{{todo.name}}&emsp;</td>
                        <td>{{todo.sifre}}&emsp;</td>
                        <td>{{todo.tarih}}&emsp;</td>
                        <td>{{todo.email}}&emsp;</td>
                        <td>{{todo.textl}}&emsp;</td>
                        <button @click="deleteTodo(todo.id)"> DELETE</button> 
                           <button @click="editTodo(todo)">EDİT</button> 
                    
                         
                          </tr>
                           </tbody>
                        </table>
                               
                        
                        
                    </div>
                </div>
                </div>
             </div>
        </div>
    </div>
  </div> 

</template>

<script>
export default {
    data() {
        return {
            isEditing: false,
            counter:0,
            name:'',
            todos:[],
            selectedTodo: null,
            
  
        }         
    },
    methods: {
        create(){
            let newTodo = {
                id:this.counter++,
                name: this.name,
                completed: false,
                sifre:this.sifre,
                tarih:this.tarih,
                email:this.email,
                textl:this.textl
               
            };
            this.todos.push(newTodo)  
            this.name=""
            this.sifre=""
            this.tarih=""
            this.email=""
            this.textl=""
        }, 
         deleteTodo (todoId) {
             let index = this.todos.findIndex(todo => {
                 return todo.id == todoId;
             });
                this.todos.splice(index,1)
        },
          updateTodo() {
              this.todos[this.selectedIndex].name = this.name;
              this.todos[this.selectedIndex].sifre = this.sifre;
              this.todos[this.selectedIndex].tarih = this.tarih;
              this.todos[this.selectedIndex].email = this.email;
              this.todos[this.selectedIndex].textl = this.textl;
              this.isEditing= false;

          },
              
          editTodo (todo) {
                this.isEditing=true;
                  let index = this.todos.findIndex(todo => {
                 return todo.id == todo.id;  
             });
                this.selectedIndex=index;
        },

          }
          
    }

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #302f2f;
  margin-top: 40px;
}
.container {
    background-color: rgb(189, 186, 186);
    
}
.text-center, .text  {
    background-color: rgb(245, 238, 225);
    font-family: "Helvetica Neue", Helvetica;
}
.btn-btn-primary {
    width: 5%;
    
}
.card-header {
    background-color: rgb(245, 238, 225);
}
</style>
