<template>
    <div>
        <div style="margin: 10px 0">
          <el-input style="width: 400px" placeholder="请输入图片url" suffix-icon="el-icon-search" v-model="url"></el-input> 
          <el-button class="ml-5" type="primary" style="margin-left:15px" @click="add" >添加</el-button>
          <el-button type="warning" @click="reset">重置</el-button>
          <br>
          <img v-if="image" :src="image"  alt="图片error" />
        </div>
       <div style="margin: 10px 0">
        <table>
    <thead>
      <tr>
        <th>日期</th>
        <th>图片URL</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in items" :key="item.date">
       <td>{{ item.date }}</td>
        <td>{{ item.url }}</td>
        <td>
          <el-button  class = "container" type="danger" icon="el-icon-delete" @click="remove(index)">删除</el-button>
        </td>
      </tr>
    </tbody>
  </table>
</div>
    </div>
  </template>

  
  <script>


  export default {
    data() {
      return {
        url : '',
        image : '',
        items: [
        {date:'',url:''},
        {date:'',url:''},
        {date:'',url:''},
        {date:'',url:''},
        {date:'',url:''}
      ]
    }
},
    methods:{
      //重置
      reset() {
        this.url = "";
      },
      add(){
        this.image = "";
        var img = new Image();
        img.src = this.url;
        img.onerror = () => {
        alert("该图片不存在");
      };
        img.onload =() =>{
          this.image = this.url;
          const now = new Date()
          const year = now.getFullYear()
          const month = now.getMonth() + 1
          const date = now.getDate()
          const hour = now.getHours()
          const minute = now.getMinutes()
          const second = now.getSeconds()
          const formattedDate = `${year}/${month}/${date} ${hour}:${minute}:${second}`
          for(var i = 0;i < 5;i++){
            if(this.items[i].url === ""){
              this.items[i] = {
                date:formattedDate,
                url:this.url
              }
              return;
            }
          }
        }
        
      },
      
      remove(index){
        this.items[index] = {
          date:"",
          url:""
        }
        this.image = "";
      }
}
  }
  </script>
  
  <style scoped>

  table{
     width :100%;
     border-collapse : collapse;
  }
  
  table, th, td {
    border: 3px solid rgb(21, 160, 165);
  }
  
  th{
   text-align:left;
   background: linear-gradient(to right, #ff7e5f, #feb47b);
   color:white;
  }
  
  td{
   padding :5px
  }
  
  tr:nth-child(even){
    padding :5px;
   background-color:#f2f2f2;
  }
  td .container {
    display: block;
    margin: 0 auto;
    padding: 10px 20px;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0,0,0,.2);
    transition: all .3s;
    height: 15vh;
    width: 25vh;
}

td .container:hover {
    box-shadow: 0 4px 8px rgba(69, 146, 82, 0.2);
}

  img {
    display: block;
    margin: 0 auto;
    padding: 20px;
    max-width: 100%;
    width: 800px;
    height: 600px;
    height: auto;
}

  </style>
