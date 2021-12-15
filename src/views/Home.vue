<template>
  <div class="home">
    <nav class="navbar navbar-expand-lg navbar-light navbar-red">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ml-auto">
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              {{user}}
            </a>
            <div class="dropdown-menu dropdown-menu-right" aria-labelledby="navbarDropdownMenuLink">
              <a class="dropdown-item" href="javascript:;">Profile</a>
              <a class="dropdown-item" href="javascript:;" @click="logout">Logout</a>
            </div>
          </li>
        </ul>
      </div>
    </nav>
    <main class="wrapper">
      <div class="sidebar">
        <ol class="mt-3">
          <li><a class="active" href="">Home</a></li>
        </ol>
      </div>
      <div class="content">
        <div class="container mt-3">
          <div class="row">
            <div class="col-lg-12 text-right mt-3">
              <button class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">Add Data</button>
            </div>
            <div v-if="success" class="col-lg-12 mt-3">
              <div class="alert alert-success alert-dismissible fade show" role="alert">
                Data Berhasil Di Tambah
                <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
            </div>
             <div v-if="error" class="col-lg-12 mt-3">
              <div class="alert alert-success alert-dismissible fade show" role="alert">
                {{msg}}
                <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
            </div>
            <div class="col-lg-12 mt-4" style="overflow-x:hidden">
              <table id="myTable" class="table table-striped w-100">
                <thead>
                  <tr>
                    <th>order id</th>
                    <th>consignee name</th>
                    <th>consignee number</th>
                    <th>consignee address</th>
                    <th>consignee postal</th>
                    <th>consignee country</th>
                    <th>consignee city</th>
                    <th>consignee state</th>
                    <th>consignee province</th>
                    <th>consignee email</th>
                    <th>length</th>
                    <th>width</th>
                    <th>height</th>
                    <th>weight</th>
                    <th>payment type</th>
                    <th>pickup contact name</th>
                    <th>pickup contact number</th>
                    <th>pickup address</th>
                    <th>pickup postal</th>
                    <th>pickup country</th>
                    <th>pickup city</th>
                    <th>pickup state</th>
                    <th>pickup province</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </main>

    <!-- Modal -->
    <div class="modal fade" data-backdrop="static" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Add New Data</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <form @submit="postData" method="POST">
            <div class="modal-body">
                <div class="form-group">
                  <label>Consignee Name <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_name" required>
                </div>
                <div class="form-group">
                  <label>Consignee Number <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_number" required>
                </div>
                <div class="form-group">
                  <label>Consignee Address <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_address" required>
                </div>
                <div class="form-group">
                  <label>Consignee Postal <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_postal" required>
                </div>
                <div class="form-group">
                  <label>Consignee Country <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_country" required>
                </div>
                <div class="form-group">
                  <label>Consignee City <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_city" required>
                </div>
                <div class="form-group">
                  <label>Consignee State <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_state" required>
                </div>
                <div class="form-group">
                  <label>Consignee Province <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.consignee_province" required>
                </div>
                <div class="form-group">
                  <label>Consignee Email <i class="text-danger">*</i></label>
                  <input type="email" class="form-control" v-model="post.consignee_email" required>
                </div>
                <div class="form-group">
                  <label>Length</label>
                  <input type="number" class="form-control" v-model="post.length">
                </div>
                <div class="form-group">
                  <label>Width</label>
                  <input type="number" class="form-control" v-model="post.width">
                </div>
                <div class="form-group">
                  <label>Height</label>
                  <input type="number" class="form-control" v-model="post.height">
                </div>
                <div class="form-group">
                  <label>Weight</label>
                  <input type="number" class="form-control" v-model="post.weight">
                </div>
                <div class="form-group">
                  <label>Payment Type</label>
                  <input type="text" class="form-control" v-model="post.payment_type">
                </div>
                <div class="form-group">
                  <label>Pickup Contact Name <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_contact_name" required>
                </div>
                <div class="form-group">
                  <label>Pickup Contact Number <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_contact_number" required>
                </div>
                <div class="form-group">
                  <label>Pickup Address <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_address" required>
                </div>
                <div class="form-group">
                  <label>Pickup Postal <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_postal" required>
                </div>
                <div class="form-group">
                  <label>Pickup Country <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_country" required>
                </div>
                <div class="form-group">
                  <label>Pickup City <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_city" required>
                </div>
                <div class="form-group">
                  <label>Pickup State <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_state" required>
                </div>
                <div class="form-group">
                  <label>Pickup Province <i class="text-danger">*</i></label>
                  <input type="text" class="form-control" v-model="post.pickup_province" required>
                </div>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
              <input type="submit" value="Save" class="btn btn-primary">
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'
import axios from 'axios'
export default {
  name: 'Home',
  data(){
    return{
      user: "",
      success: false,
      error: false,
      msg: "",
      post: {
        consignee_name : null,
        consignee_number: null,
        consignee_address: null,
        consignee_postal: null,
        consignee_country: null,
        consignee_city: null,
        consignee_state: null,
        consignee_province: null,
        consignee_email: null,
        length: null,
        width: null,
        height: null,
        weight: null,
        payment_type: null,
        pickup_contact_name: null,
        pickup_contact_number: null,
        pickup_address: null,
        pickup_postal: null,
        pickup_country: null,
        pickup_city: null,
        pickup_state: null,
        pickup_province: null
      }
    }
  },
  mounted(){
    this.user = localStorage.getItem('user')
    this.getData()
  },
  methods: {
    getData: function(){
      axios.get('https://frontend-screening-v1.herokuapp.com/order', {
        headers: {
          'Authorization': localStorage.getItem('token'),
          'Content-Type': 'application/json'
        }
      })
      .then(function (response) {
        $('#myTable').DataTable({
          scrollX: true,
          data: response.data.data,
          columns: [
            { data : 'order_id'},
            { data : 'consignee_name'},
            { data : 'consignee_number'},
            { data : 'consignee_address'},
            { data : 'consignee_postal'},
            { data : 'consignee_country'},
            { data : 'consignee_city'},
            { data : 'consignee_state'},
            { data : 'consignee_province'},
            { data : 'consignee_email'},
            { data : 'length'},
            { data : 'width'},
            { data : 'height'},
            { data : 'weight'},
            { data : 'payment_type'},
            { data : 'pickup_contact_name'},
            { data : 'pickup_contact_number'},
            { data : 'pickup_address'},
            { data : 'pickup_postal'},
            { data : 'pickup_country'},
            { data : 'pickup_city'},
            { data : 'pickup_state'},
            { data : 'pickup_province'},
          ]
        });
      })
      .catch(function (error) {
        console.log(error);
      }) 
    },
    postData: function(e){
      e.preventDefault()
      axios.post('https://frontend-screening-v1.herokuapp.com/order', this.post, {
        headers:{
          'Authorization': localStorage.getItem('token'),
          'Content-Type': 'application/json'
        }
      })
      .then((response) => {
          this.post.consignee_name  = null,
          this.post.consignee_number = null,
          this.post.consignee_address = null,
          this.post.consignee_postal = null,
          this.post.consignee_country = null,
          this.post.consignee_city = null,
          this.post.consignee_state = null,
          this.post.consignee_province = null,
          this.post.consignee_email = null,
          this.post.length = null,
          this.post.width = null,
          this.post.height = null,
          this.post.weight = null,
          this.post.payment_type = null,
          this.post.pickup_contact_name = null,
          this.post.pickup_contact_number = null,
          this.post.pickup_address = null,
          this.post.pickup_postal = null,
          this.post.pickup_country = null,
          this.post.pickup_city = null,
          this.post.pickup_state = null,
          this.post.pickup_province = null

        if(response){
          $('#exampleModal').modal('hide')
          $('#myTable').DataTable().destroy();
          $('#myTable tbody').empty();
          this.getData()
          this.success = true
        }
      })
      .catch((error) => {
       if(error){
         this.error = true
         this.msg = error.response.data.message
       }
      });
    },
    logout: function(){
      localStorage.removeItem('user')
      localStorage.removeItem('token')
      this.$router.push({name: 'Login'})
    }
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  font-size: 15px;
}
body{
  background-color: #f8f9fc!important;
  height: 100%;
  display: flex;
  flex-direction: column;

}
.navbar-red{
  background: #FFFFFF;
  padding-top: 20px!important;
  padding-bottom: 20px!important;
  border-bottom: 2px solid #F5F5F5;

}
.wrapper{
  display: flex;
}
.sidebar{
  width: 273px;
  background: #4e73df;
  min-height: 100vh;
  padding: 20px 0;
}
.sidebar ol{
  padding: 0;
  list-style: none;
}
.sidebar ol li a{
  padding: 10px 20px;
  font-size: 16px;
  display: flex;
  color: #FFFFFF;
}
.sidebar ol li a:hover{
  text-decoration: none;
}
.sidebar ol li a.active{
  background: #f8f9fc;
  color: #4e73df;
}
.content{
  width: 100%;
}
.table-striped thead tr th{
  min-width: 200px;
}
</style>
