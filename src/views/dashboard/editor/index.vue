<template>
	<div class="dashboard-editor-container">
		<el-row class="btn-group">
			<el-col :span="4" class='text-center'>
				<router-link class="pan-btn blue-btn" to="/components/index">Components</router-link>
			</el-col>
			<el-col :span="4" class='text-center'>
				<router-link class="pan-btn light-blue-btn" to="/charts/index">Charts</router-link>
			</el-col>
			<el-col :span="4" class='text-center'>
				<router-link class="pan-btn pink-btn" to="/excel/download">Excel</router-link>
			</el-col>
			<el-col :span="4" class='text-center'>
				<router-link class="pan-btn green-btn" to="/example/table/table">Table</router-link>
			</el-col>
			<el-col :span="4" class='text-center'>
				<router-link class="pan-btn tiffany-btn" to="/example/form/edit">Form</router-link>
			</el-col>
			<el-col :span="4" class='text-center'>
				<router-link class="pan-btn yellow-btn" to="/example/form/edit">Theme</router-link>
			</el-col>
		</el-row>

		<el-row>
			<el-col :span="6">
				<el-card class="box-card">
					<div slot="header" class="box-card-header">
						<pan-thumb class="panThumb" :image="avatar"> 你的权限:
							<span class="pan-info-roles" :key='item' v-for="item in auths">{{item}}</span>
						</pan-thumb>
					</div>
					<span class="display_name">{{userName}}</span>
					<div class="info-item">
						<countTo class="info-item-num" :startVal='0' :endVal='statisticsData.article_count' :duration='3400'></countTo>
						<span class="info-item-text">文章</span>
						<icon-svg icon-class="a" class="dashboard-editor-icon"></icon-svg>
					</div>
					<div class="info-item">
						<countTo class="info-item-num" :startVal='0' :endVal='statisticsData.pageviews_count' :duration='3600'></countTo>
						<span class="info-item-text">浏览量</span>
						<icon-svg icon-class="b" class="dashboard-editor-icon"></icon-svg>
					</div>
				</el-card>
			</el-col>

			<el-col :span="8">
				<pie-chart></pie-chart>
			</el-col>

			<el-col :span="10">
				<bar-chart></bar-chart>
			</el-col>
		</el-row>
	</div>
</template>

<script>
	import { mapGetters } from 'vuex';
	import panThumb from 'components/PanThumb';
	import pieChart from './pieChart';
	import barChart from './barChart';
    import countTo from 'vue-count-to';
	export default {
	  name: 'dashboard-editor',
	  components: { panThumb, pieChart, barChart, countTo },
	  data() {
    return {
	      statisticsData: {
	        article_count: 1024,
	        comment_count: 102400,
	        latest_article: [],
	        month_article_count: 28,
	        pageviews_count: 1024
      }
    }
  },
	  computed: {
	    ...mapGetters([
	      'userName',
	      'userId',
	      'avatar',
	      'auths'
    ])
  }
	}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.dashboard-editor-container {
    margin: 30px;
    .btn-group {
        margin-bottom: 60px;
    }
    .box-card-header {
        position: relative;
        height: 160px;
    }
    .panThumb {
        z-index: 100;
        height: 150px;
        width: 150px;
        position: absolute;
        left: 0px;
        right: 0px;
        margin: auto;
    }
    .display_name{
        font-size: 30px;
        display: block;
    }
    .info-item{
        display: inline-block;
        margin-top: 10px;
        font-size: 14px;
        &:last-of-type{
            margin-left: 15px;
        }
    }
}
</style>
