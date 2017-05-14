<template>
  <div class="hello">
    <h1>身　高:   <input type="text" v-model="height" />cm</h1>
    <h1>體　重:   <input type="text" v-model="weight" />kg</h1>
    <h1>ＢＭＩ： {{  weight /((height/100)*(height/100)) }}</h1>
    <h2></h2> {{test}}
    <p>
      <el-button @click="callme" type="primary">我是按鈕</el-button>
    </p>
  
    <el-table v-loading.body="loading" :data="posts" border style="width: 100%" :default-sort="{prop: 'id', order: 'descending'}">
      <el-table-column prop="first_name" label="first_name" sortable width="180">
      </el-table-column>
      <el-table-column prop="last_name" label="last_name" sortable width="180">
      </el-table-column>
      <el-table-column prop="SexName" label="性別" sortable width="50">
      </el-table-column>
      <el-table-column prop="phone_number" label="phone_number" sortable width="180">
      </el-table-column>
      <el-table-column prop="email" label="email" sortable width="220">
      </el-table-column>
      <el-table-column prop="address_1" label="address_1" sortable>
      </el-table-column>
    </el-table>
    <el-pagination @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="currentPage4" :page-sizes="[100, 200, 300, 400]" :page-size="100" layout="total, sizes, prev, pager, next, jumper" :total="400">
    </el-pagination>
  
    <el-checkbox v-model="checked">备选项</el-checkbox>
    <el-button @click="created" type="primary">主要按钮</el-button>
    <el-table :data="gridData" border style="width: 100%" :default-sort="{prop: 'userId', order: 'descending'}">
      <el-table-column prop="Cre_Date_" label="Cre_Date_" sortable width="200">
      </el-table-column>
      <el-table-column prop="StatusName_" label="StatusName_" sortable width="300">
      </el-table-column>
      <el-table-column prop="BeforeDesc_" label="BeforeDesc_" sortable>
      </el-table-column>
  
    </el-table>
    <table>
      <thead>
        <tr rowspan="1" colspan="1" style="width: 262.5px;">
          Name
  
        </tr>
      </thead>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'hello',
  data() {
    return {
      height: 0,
      weight: 0,
      test: 0,
      msg: 'Welcome to Your Vue.js App',
      dismissCountDown: null,
      showDismissibleAlert: false,
      checked: true,
      apiUrl: 'https://jsonplaceholder.typicode.com/posts',
      apiUrl2: 'http://work1999.kcg.gov.tw/open1999/ServiceRequestsQuery.asmx/ServiceRequestsQuery',
      apiUrl3: '?SN=n1oOkV$gy2YXqPriGaYUcQ@@',
      apiPos: 'http://localhost:32787/api/pos/GetOsposPeople',
      gridData: [],
      posts: [],
      loading: false
    }
  },
  methods: {
    callme2() {
      this.test = this.test + 1
    },
    callme() {
      this.loading = true
      axios.get(this.apiPos)
        .then(response => {
          this.posts = response.data
          this.loading = false
        })
        .catch(e => {
          this.errors.push(e)
          this.loading = false
        })
    },


    countDownChanged(dismissCountDown) {
      this.dismissCountDown = dismissCountDown;
    },
    showAlert() {
      this.dismissCountDown = 5;
    },
    created() {
      axios.get(this.apiUrl3)
        .then(response => {
          // JSON responses are automatically parsed.
          this.gridData = response.data
          console.log(this.gridData);
        })
        .catch(e => {
          this.errors.push(e)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass">



@mixin text($font-size: 30px,$color: red,$letter-spacing: 20px)
  font-size: $font-size
  color: $color
  letter-spacing: 20px
h1
  +text(50px,block,40px)
  font-family: 微軟正黑體
h2
  +text
  font-family: 微軟正黑體
table
  // display: block
  // color: #514d6a
  // border-color: grey
  // border-top-color: grey
  // border-right-color: grey
  // border-bottom-color: grey
  // border-left-color: grey
  // border-spacing: 2px
  line-height: 1.5
  border-bottom: 1px solid #e4e9f0

// h1, h2 {
//   font-weight: normal;
// }

// ul {
//   list-style-type: none;
//   padding: 0;
// }

// li {
//   display: inline-block;
//   margin: 0 10px;
// }

// a {
//   color: #42b983;
// }
</style>
