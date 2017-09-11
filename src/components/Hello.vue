<template>
  <div class="hello">
    <div class="container">
      <div class="head bb">
        <div class="content">
          <div class="topgrid flex">
            <div class="left flex">
              <div class="logo">狗</div>
            </div>
            <div class="right flex">
              <div class="ad">廣告</div>
            </div>
          </div>
          <div class="botgrid">
            <div class="left">

            </div>
            <div class="right">

            </div>
          </div>
        </div>
      </div>
      <div class="map bb flex">
        <div class="content">
          <div class="left">
            <h2>我在哪</h2>
          </div>
          <div class="right">
            <div class="hosdata">
              <select class="" name="" v-model="pickarea">
                <option v-for="n in arealist">{{n}}</option>
              </select>
              <button type="button" name="button" @click="getnews">動物醫院在哪</button>
              <div class="" v-for="item in datatext">
                  <h3>地區：{{item.area}}</h3>
                  <h3>醫院名稱：{{item.name}}</h3>
                  <h3>醫院地址：{{item.address}}</h3>
                  <h3>醫院電話：{{item.number}}</h3>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="box bb">
        <div class="content">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery'
window.$ = $

export default {
  name: 'hello',
  data () {
    return {
      arealist: ['台北市', '台南市'],
      pickarea: [],
      datatext: []
    }
  },
  methods: {
    // 取得醫院資料
    getnews: function () {
      console.log(this.pickarea)
      $.ajax({
        url: 'http://13.114.3.214/api/v1/animalhospital?page=&area={{this.pickarea}}&name=',
        type: 'GET',
        mode: 'no-cors',
        success: function (res) {
          this.datatext = res.data
          console.log(this.datatext)
        }.bind(this),
        error: function (xhr, ajaxOptions, thrownError) {
          console.log('fail')
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

$colorbw:#f9f8f3;

.bb{
  border:1px solid #030303;
}
.flex{
  display:flex;
}

.head{
  .content{
    width:100%;
  }
  .topgrid{
    width:100%;
    .left{
      flex:2;
    }
    .right{
      flex:6;
    }
    .logo{
      width:100%;
      text-align: center;
      justify-content: flex-start;
      align-items: center;
      padding:2%;
    }
    .ad{
      width:100%;
      text-align: center;
      justify-content: center;
      align-items: center;
      padding:2%;
    }
  }
}
.map{
  .content{
    width:100%;
    background-color:$colorbw;
  }
}
h1, h2 {
  font-weight: normal;
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
</style>
