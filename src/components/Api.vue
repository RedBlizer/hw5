<template>
  <div id="body">
    <h2>瑞穗鮮乳</h2>

    <form id="cpi" >
      <label for="date">Date</label>
      <input type="text" id="date" name="date">
      <label for="name">Name</label>
      <input type="text" id="name" name="name">
      <label for="price">Price</label>
      <input type="text" id="price" name="price">

      <button type="submit">Submit</button>
    </form>


    <div id="app">
      <button v-on:click="handleClick">顯示資料</button>
      <table>
        <thead>
        <tr>
          <th>date</th>
          <th>name</th>
          <th>price</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="item in data">
          <td>{{ item.date }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.price }}</td>
        </tr>
        </tbody>
      </table>
    </div>

    <p id="log"></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: []
    };
  },
  methods: {
    async handleClick() {
      console.log("data");

      const url = "http://localhost:3000/api"; // 資料傳送到的 URL
      try {
        const response = await fetch(url, {
          method: 'GET',
        });
        const res_data = await response.json();
        this.data = res_data ;
        // 在這裡處理回應資料，例如顯示成功訊息或更新頁面內容
        console.log("成功", res_data );
      } catch (error) {
        // 在這裡處理錯誤，例如顯示錯誤訊息或者回滾操作
        console.log("錯誤", error);
      }
    }
  }
}

</script>


<style scoped>

#body{
  text-align:center;
}

input{
  height:30px;
}

button{
  color:blue;
  background-color: #e8bfbf;
  height:40px;
  width:100px;
}

table{
  padding: 20px;
  width:400px;
  margin-left:auto;
  margin-right:auto;
}
th , td{
  border:3px solid black;
  width:100px;
}
th{
  background-color:green;
  color:white;
}
</style>