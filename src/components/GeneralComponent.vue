<template>
  <div class="hello">
    <el-card class="box-card">
      <div class="block">
        <form action="">

        </form>
      </div>
      <div class="block">
        <template>
          <el-table
              :data="pages"
              style="width: 100%">
            <el-table-column
                prop="ImagePath"
                label="Avatar">

            </el-table-column>
            <el-table-column
                prop="CreatorName"
                label="Name">
            </el-table-column>
            <el-table-column
                prop="Total"
                label="Total">
            </el-table-column>
          </el-table>
        </template>
      </div>
    </el-card>
  </div>
</template>

<script>
import * as axios from "axios";

const API_URL = "https://api.gofundraise.com.au/v1/pages/search?";

export default {
  name: 'GeneralComponent',
  props: {
    msg: String
  },
  data: () => ({
    pages: []
  }),
  methods: {
    getData() {
      axios.get(API_URL + "eventcampaignid=1&pagetype=T&sortorder=desc&sortby=4&pagesize=5").then((data)=> {
        this.pages = data.data.Pages;
      })

    }
  },
  mounted() {
    this.getData();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
