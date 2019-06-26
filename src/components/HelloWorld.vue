<template>
 <div class="hello">
   <h1 class="header">Add New Restaurant</h1>
                <!--add new form-->
                <form class="addnewform"  >
                    <div class="form-group row">
                        <label for="r_name" class="col-sm-2 col-form-label">Resturant Name :</label>
                        <div class="col-sm-8"><input type="text" class="form-control" placeholder="Resturant Name here.." v-model="r_name"></div>
                    </div>
                    <div class="form-group row">
                        <label for="location" class="col-sm-2 col-form-label">Location :</label>
                        <div class="col-sm-8"><input type="text" class="form-control" placeholder="eg : city walk, andheri, mumbai.." v-model="city"></div>
                    </div>
                    <div class="form-group row">
                        <label for="cusine" class="col-sm-2 col-form-label">Cusine :</label>
                        <div class="col-sm-8"><input type="text" class="form-control" placeholder="eg : Cusine" v-model="cusine"></div>
                    </div>
                    <div class="form-group row">
                        <label for="p_no" class="col-sm-2 col-form-label">Phone Number :</label>
                        <div class="col-sm-8"><input type="text" class="form-control" placeholder="eg : 8596325471" v-model="p_no"></div>
                    </div>
                    <div class="form-group row">
                        <label for="rating" class="col-sm-2 col-form-label">rating :</label>
                        <div class="col-sm-8"><input type="text" class="form-control" placeholder="eg : 4.5" v-model="rating"></div>
                    </div>
                </form>

                <form @submit.prevent="additem()">
                  <div class="menu addnewform" >
                    <h1>Menu : </h1>
                   <!-- <div class="menu-item" v-for="post of posts" v-bind:key="post.id">
                        <div class="row" v-for="menu in post.menu" :key="menu.id">
                            <div class="col-md-4" >
                                <div >{{menu.name}}</div>
                            </div>
                            <div class="col-md-4">
                                <div>{{menu.price}}</div>
                            </div>
                            <div class="col-md-4">
                                <button class="delete btn btn-warning">X</button>
                            </div>
                        </div>
                    </div>-->

                    <div class="menu-item" >
                        <div class="row">
                            <div class="col-md-4" >
                                <div>
                                  <li v-for="todo in todos" v-bind:key="todo.key">{{todo.item}}</li>
                                </div>
                            </div>
                            <div class="col-md-4">
                                <div><li v-for="todo in todos" v-bind:key="todo.key">{{todo.price}}</li></div>
                            </div>
                            <div class="col-md-4">
                                <button class="delete btn btn-warning">X</button>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="add-item addnewform">
                    <div class="row">
                            <div class="col-md-4">
                                <input type="text" class="form-control" placeholder="Menu Item" v-model="menuitem">
                            </div>
                            <div class="col-md-4">
                                <input type="text" class="form-control" placeholder="Price" v-model="menuprice">
                            </div>
                            <div class="col-md-4">
                                <button type="submit" class="additem btn btn-success" @click="display()">+</button>
                            </div>
                        </div>
                </div>
                </form>

                <div class="save mt-3">
                    <button type="submit" class="btn btn-success btn-lg m-2" @click="postpost()">SAVE</button>
                    <button class="btn btn-danger btn-lg">CANCEL</button>
                    </div>
                     
                </div>

</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  props: {
    
  },
  data(){
    return {
      posts : [],
      names : [],
      output : [],
      r_name : '',
      city : '',
      cusine : '',
      p_no : '',
      rating : '',
      menuitem : '',
      menuprice : '',
      todos : []
      
    }
  },
  methods: {
    postpost(){
        axios.post('http://localhost:3000/restaurant',{
          name :this.r_name,
          location : this.city,
          cusine : this.cusine,
          phone : this.p_no,
          rating : this.rating,
          menu : [{name : this.menuitem, price :this.menuprice}]
      },{
        headers: {
            'Content-Type': 'application/json',
        }
      }).then((response) => {})
      .catch((e) => {
        console.error(e)
      })
    },
    additem(){
    this.todos.push({item : this.menuitem, price : this.menuprice}),
    console.log(todos)
  },
  created(){
    axios.get('http://localhost:3000/restaurant')
    .then(response => {
      this.posts = response.data
    })
  },
  display(){
    
  }
}
  }
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello{
      text-align: center;
      font-family:'Righteous', cursive;
      background-color:#fcf8f4;
      min-height:100vh;
      height:100%;
}

/*header*/
.header{
    font-size:8vh;
    /*background-color:#f2d7a4;*/
    padding:40px;
    font-family:'Righteous', cursive;
    background-image:url('../assets/addnewbg.jpg');
    background-position: center;
}

            .addnewform{
                width:70%;
                margin:auto;
                padding:20px;
            }
</style>
