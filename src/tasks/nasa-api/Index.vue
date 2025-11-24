<template>
  <div class="card d-print-none mb-2" >
    <div class="card-header d-print-none">
      {{labels.get('label_task')}}
    </div>
    <div class="card-body">
      <div class="row">
        <div class="col-lg-4">
          <div class="input-group mb-3">
            <input type="date" id="date" class="form-control" placeholder="Select Date">
            <div class="input-group-append">
              <button class="btn btn-primary" type="button" @click="ShowData">Show Data</button>
            </div>
          </div>
        </div>
      </div>
      <div class="row" v-if="item.exists">
        <div class="col-12">
          <table>
            <tbody>
              <tr>
                <td>Title</td>
                <td>{{item.data.title}}</td>
              </tr>
              <tr>
                <td>Description</td>
                <td>{{item.data.explanation}}</td>
              </tr>
            </tbody>
          </table>
          <img style="max-width:100%;" alt="Vue logo" :src="item.data.hdurl">
        </div>
      </div>

    </div>
  </div>
</template>
<script setup>
  import globalVariables from "@/assets/globalVariables";
  import systemFunctions from "@/assets/systemFunctions";
  import toastFunctions from "@/assets/toastFunctions";
  import labels from '@/labels'
  import { reactive } from 'vue'
  import {useRouter} from 'vue-router';
  import axios from 'axios';
  const router =useRouter()
  let taskData=reactive({
    taskBaseUrl:systemFunctions.getTaskBaseURL(import.meta.url),
  })
  let item=reactive({
    exists:false,
    data:{
    }
  })
  labels.add([{language:globalVariables.language,file:'tasks'+taskData.taskBaseUrl+'/labels.js'}])


  const ShowData=async ()=>{
    item.exists=false;
    let date=$('#date').val();
    //let apiKey='DEMO_KEY';
    let apiKey='4VzgsuIglUPOu5xRooYCx6aIIvYaizihhlSQTwYX'
    await axios.get('https://api.nasa.gov/planetary/apod?api_key='+apiKey+'&date='+date).then((res)=>{
      if (res.data) {
        globalVariables.loadListData=true;
        item.data=res.data;
        item.exists=true;
      }
      else{
        toastFunctions.showResponseError(res.data)
      }
    });
  }
</script>


<style  scoped>
.main {
   height: auto;
}



.login-left > img {
  margin-left: 12%;
}

.center-align {
  /*margin-top: 20vh;*/
  margin-right: 0;
  margin-left: 0;
}

.center-align > div{
  margin-top: 20vh;
}

.bg-authentication {
  background-color: #eff2f7;
}
.input-group-text {
  background-color: #ffffff;
}
.bg-authentication .login-footer {
  padding: 0 1.5rem 3.5rem;
}
@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {
  .bg-authentication {
    width: 100%;
  }
  .center-align {
    margin-top: 20vh;
  }
}
</style>
