<template>
  <div class="hello">
    <el-card class="box-card">
      <div class="block">
        <el-form :inline="true" :model="formInline" class="demo-form-inline">
          <el-form-item label="Event ID">
            <el-input v-model="formInline.eventId" placeholder="Event ID"></el-input>
          </el-form-item>
          <el-form-item label="Elements quality">
            <el-input v-model="formInline.pageSize" placeholder="Quality"></el-input>
          </el-form-item>
          <el-form-item label="Page type">
            <el-select v-model="formInline.pageType" placeholder="Team or Single">
              <el-option label="Team" value="T"></el-option>
              <el-option label="Single" value="S"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="getData">Query</el-button>
          </el-form-item>
        </el-form>
      </div>
      <div class="block">
        <template>
          <el-table
              :data="pages"
              style="width: 100%">
              <el-table-column prop="ImagePath"
                               label="Avatar">
                <template slot-scope="scope">
                  <el-avatar size="large" :src="scope.row.ImagePath"></el-avatar>
                </template>
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
    pages: [],
    formInline: {
      eventId: '1',
      pageType: 'S',
      pageSize: '5',
    }
  }),
  methods: {
    getData() {
      console.log(this.formInline);
      axios.get(API_URL + `eventcampaignid=${this.formInline.eventId}&pagetype=${this.formInline.pageType}` +
      `&sortorder=desc&sortby=4&pagesize=${this.formInline.pageSize}`).then((data)=> {
        this.pages = data.data.Pages;
      })

    }
  },
  mounted() {
    setTimeout(()=> {
      this.getData();
    },10000)

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
