<template>
    <div class="dashboard-content">
        <el-card>
            <div slot="header">
                <span style="font-size: 23px;"><i class="fa fa-pie-chart"></i>dashboard</span>
                <el-select size="small" class="pull-right" v-model="clusterKey" @change="clusterChange">
                    <el-option label="全部集群" value=""></el-option>
                    <el-option v-for="item in clusterKeys" :label="item" :value="item" :key="item"></el-option>
                </el-select>
            </div>
            <div>
                <el-row :gutter="20">
                    <el-col :span="8">
                        <CardPanel type="primary" icon="fa fa-navicon" title="总域数" :num="domainCount" to-url="domain_statistic" :url-query="clusterKey"></CardPanel>
                    </el-col>
                    <el-col :span="8">
                        <CardPanel type="green" icon="fa fa-server" title="Executor数: 物理机+容器" :num="executorCount" to-url="executor_statistic" :url-query="clusterKey"></CardPanel>
                    </el-col>
                    <el-col :span="8">
                        <CardPanel type="yellow" icon="fa fa-cubes" title="总作业数" :num="jobCount" to-url="job_statistic" :url-query="clusterKey"></CardPanel>
                    </el-col>
                </el-row>
            </div>
        </el-card>
    </div>
</template>
<script>
export default {
  props: [],
  data() {
    return {
      clusterKey: '',
      clusterKeys: [],
      domainCount: '',
      executorInDockerCount: '',
      executorNotInDockerCount: '',
      jobCount: '',
    };
  },
  methods: {
    clusterChange() {
      this.getDashboardCount();
    },
    getDashboardCount() {
      let url = '';
      if (this.clusterKey !== '') {
        url = `/console/zkClusters/${this.clusterKey}/dashboard/count`;
      } else {
        url = '/console/zkClusters/dashboard/count';
      }
      this.$http.get(url).then((data) => {
        this.domainCount = data.domainCount;
        this.executorInDockerCount = data.executorInDockerCount;
        this.executorNotInDockerCount = data.executorNotInDockerCount;
        this.jobCount = data.jobCount;
      })
      .catch(() => { this.$http.buildErrorHandler('获取dashboard统计请求失败！'); });
    },
    getZkClusters() {
      this.$http.get('/console/zkClusters/zkClusterKeys').then((data) => {
        this.clusterKeys = data;
      })
      .catch(() => { this.$http.buildErrorHandler('获取所有zk集群请求失败！'); });
    },
  },
  computed: {
    executorCount() {
      return `${this.executorNotInDockerCount}+${this.executorInDockerCount}`;
    },
  },
  created() {
    this.getZkClusters();
    this.getDashboardCount();
  },
};
</script>
<style lang="sass" scoped>
.dashboard-content {
    margin: 20px;
}
</style>
