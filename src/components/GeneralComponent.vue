<template>
  <div class="hello">
    <el-card class="box-card">
      <div class="block">
        <el-form :inline="true" :model="formInline" class="demo-form-inline">
          <el-form-item label="Event ID">
            <el-input v-model="formInline.eventId" placeholder="Event ID"/>
          </el-form-item>
          <el-form-item label="Elements quality">
            <el-input v-model="formInline.pageSize" placeholder="Quality"/>
          </el-form-item>
          <el-form-item label="Page type">
            <el-select v-model="formInline.pageType" placeholder="Team or Single">
              <el-option label="Team" value="T"/>
              <el-option label="Single" value="S"/>
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="getData">Query</el-button>
          </el-form-item>
          <el-form-item>
            <el-tooltip effect="dark" content="Fon-size in table" placement="top-start">
              <el-select v-model="textStyles.baseFontSize" placeholder="Base fontsize">
                <el-option v-for="item in fontSizes" :key="item" :label="item" :value="item"/>
              </el-select>
            </el-tooltip>
          </el-form-item>
          <el-form-item>
            <el-tooltip effect="dark" content="Name text color" placement="top-start">
              <el-color-picker v-model="textStyles.nameColor"/>
            </el-tooltip>
          </el-form-item>
          <el-form-item>
            <el-tooltip effect="dark" content="Total text color" placement="top-start">
              <el-color-picker v-model="textStyles.totalColor"/>
            </el-tooltip>
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
              <template slot-scope="scope">
                <span :style="'color:'+ textStyles.nameColor + ';font-size:' + textStyles.baseFontSize + 'px'">{{scope.row.CreatorName}}</span>
              </template>
            </el-table-column>
            <template v-if="this.currentPageType === 'S'">
              <el-table-column
                  prop="Total"
                  label="Total">
                <template slot-scope="scope">
                  <span :style="'color:'+ textStyles.totalColor + ';font-size:' + textStyles.baseFontSize + 'px'">{{scope.row.Total }}</span>
                </template>
              </el-table-column>
            </template>
            <template v-else>
              <el-table-column
                  prop="Team.TeamTotal"
                  label="Team total">
                <template slot-scope="scope">
                  <span :style="'color:'+ textStyles.totalColor + ';font-size:' + textStyles.baseFontSize + 'px'">{{scope.row.Team.TeamTotal }}</span>
                </template>
              </el-table-column>
            </template>
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
    fontSizes: [10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26],
    formInline: {
      eventId: '1',
      pageType: 'S',
      pageSize: '5',
    },
    textStyles: {
      baseFontSize: '16',
      nameColor: "#111111",
      totalColor: "#111111"
    },
    currentPageType: "S"
  }),
  methods: {
    getData() {
      console.log(this.textStyles);
      this.currentPageType = this.formInline.pageType;
      axios.get(API_URL + `eventcampaignid=${this.formInline.eventId}&pagetype=${this.formInline.pageType}` +
          `&sortorder=desc&sortby=4&pagesize=${this.formInline.pageSize}`).then((data) => {
        this.pages = [];
        this.pages = data.data.Pages;
      })

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
