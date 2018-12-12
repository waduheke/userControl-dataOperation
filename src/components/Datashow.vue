<template>
  <div class="content">
    <div class="head">
      <el-tabs width="100%" @tab-click="switchdata">
        <el-tab-pane label="IPV4展示">
          <el-table :data="currentData" border style="width:100%">
            <el-table-column prop="ip" label="IP地址"></el-table-column>
            <el-table-column prop="mac" label="MAC地址"></el-table-column>
          </el-table>
          <div class="page-number">
            <el-pagination
              @size-change="handleSizeChange"
              @current-change="handleCurrentChange"
              :current-page="currentPage"
              :page-sizes="[40, 50, 60, 70]"
              :page-size="prePageSize"
              layout="total, sizes, prev, pager, next, jumper"
              :total="totalNumber">
            </el-pagination>
          </div>
        </el-tab-pane>
        <el-tab-pane label="IPV6展示">
          <el-table :data="currentData" border style="width:100%">
            <el-table-column prop="ip" label="IP地址"></el-table-column>
            <el-table-column prop="mac" label="MAC地址"></el-table-column>
          </el-table>
          <div class="page-number">
            <el-pagination
              @size-change="handleSizeChange"
              @current-change="handleCurrentChange"
              :current-page="currentPage"
              :page-sizes="[40, 50, 60, 70]"
              :page-size="prePageSize"
              layout="total, sizes, prev, pager, next, jumper"
              :total="totalNumber">
            </el-pagination>
          </div>
        </el-tab-pane>
      </el-tabs>
    </div>
    <div class="form"></div>
    <div class="page-and-backtop">
      <div class="page"></div>
      <div class="backtop"></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Datashow',
  data: function(){
    return {
      pack:['{"ip": "192.168.100.68", "mac": " 0:0:0:0:0:0"}', '{"ip": "192.168.100.90", "mac": " 0:1a:a9:c5:55:33"}', '{"ip": "192.168.100.91", "mac": " 0:1a:a9:c5:5a:e7"}', '{"ip": "192.168.100.92", "mac": " 0:1a:a9:c5:5b:21"}', '{"ip": "192.168.100.93", "mac": " 0:1a:a9:c5:55:49"}', '{"ip": "192.168.100.94", "mac": " 0:1a:a9:c5:53:d3"}', '{"ip": "192.168.100.95", "mac": " 14:14:4b:19:e2:b"}', '{"ip": "192.168.100.101", "mac": " 14:14:4b:60:44:a5"}', '{"ip": "192.168.100.102", "mac": " 58:69:6c:35:6e:f0"}', '{"ip": "192.168.100.103", "mac": " 58:69:6c:35:70:10"}', '{"ip": "192.168.100.104", "mac": " 58:69:6c:35:6c:c0"}', '{"ip": "192.168.100.105", "mac": " 58:69:6c:35:6f:16"}', '{"ip": "192.168.100.106", "mac": " 58:69:6c:35:6f:58"}', '{"ip": "192.168.100.107", "mac": " 58:69:6c:35:6b:96"}', '{"ip": "192.168.100.108", "mac": " 58:69:6c:35:6a:b6"}', '{"ip": "192.168.100.123", "mac": " 0:1a:a9:1f:a1:b1"}', '{"ip": "192.168.100.124", "mac": " 0:1a:a9:c4:85:5b"}', '{"ip": "192.168.100.125", "mac": " 0:1a:a9:c4:7f:b"}', '{"ip": "192.168.100.126", "mac": " 0:1a:a9:c4:61:67"}', '{"ip": "192.168.100.127", "mac": " 0:1a:a9:c4:88:97"}', '{"ip": "192.168.100.128", "mac": " 58:69:6c:35:71:a4"}', '{"ip": "192.168.100.131", "mac": " 0:1a:a9:1c:14:59"}', '{"ip": "192.168.100.132", "mac": " 0:1a:a9:1c:3c:59"}', '{"ip": "192.168.100.133", "mac": " 0:1a:a9:1c:1f:99"}', '{"ip": "192.168.100.134", "mac": " 0:1a:a9:1c:10:19"}', '{"ip": "192.168.100.135", "mac": " 0:1a:a9:bc:38:6b"}', '{"ip": "192.168.100.141", "mac": " 0:1a:a9:1f:a1:b5"}', '{"ip": "192.168.100.142", "mac": " 0:1a:a9:1e:d4:15"}', '{"ip": "192.168.100.143", "mac": " 0:1a:a9:46:e6:d6"}', '{"ip": "192.168.100.144", "mac": " 0:1a:a9:46:e7:50"}', '{"ip": "192.168.100.150", "mac": " 58:69:6c:8e:d7:f0"}', '{"ip": "192.168.100.151", "mac": " 58:69:6c:8e:e6:0"}', '{"ip": "192.168.100.152", "mac": " 58:69:6c:8e:e3:60"}', '{"ip": "192.168.100.155", "mac": " 58:69:6c:8e:e3:24"}', '{"ip": "192.168.100.156", "mac": " 58:69:6c:8e:e3:62"}', '{"ip": "192.168.100.157", "mac": " 58:69:6c:8e:e6:5e"}', '{"ip": "192.168.100.201", "mac": " 14:14:4b:1b:91:57"}', '{"ip": "210.45.241.2", "mac": " 0:9:6b:71:a4:be"}', '{"ip": "210.45.241.3", "mac": " 0:90:fb:30:95:6d"}', '{"ip": "210.45.241.4", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.5", "mac": " 0:1e:b:c5:38:3a"}', '{"ip": "210.45.241.6", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.12", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.14", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.16", "mac": " 0:25:90:9d:28:24"}', '{"ip": "210.45.241.25", "mac": " 6c:92:bf:32:c7:fc"}','{"ip": "192.168.100.68", "mac": " 0:0:0:0:0:0"}', '{"ip": "192.168.100.90", "mac": " 0:1a:a9:c5:55:33"}', '{"ip": "192.168.100.91", "mac": " 0:1a:a9:c5:5a:e7"}', '{"ip": "192.168.100.92", "mac": " 0:1a:a9:c5:5b:21"}', '{"ip": "192.168.100.93", "mac": " 0:1a:a9:c5:55:49"}', '{"ip": "192.168.100.94", "mac": " 0:1a:a9:c5:53:d3"}', '{"ip": "192.168.100.95", "mac": " 14:14:4b:19:e2:b"}', '{"ip": "192.168.100.101", "mac": " 14:14:4b:60:44:a5"}', '{"ip": "192.168.100.102", "mac": " 58:69:6c:35:6e:f0"}', '{"ip": "192.168.100.103", "mac": " 58:69:6c:35:70:10"}', '{"ip": "192.168.100.104", "mac": " 58:69:6c:35:6c:c0"}', '{"ip": "192.168.100.105", "mac": " 58:69:6c:35:6f:16"}', '{"ip": "192.168.100.106", "mac": " 58:69:6c:35:6f:58"}', '{"ip": "192.168.100.107", "mac": " 58:69:6c:35:6b:96"}', '{"ip": "192.168.100.108", "mac": " 58:69:6c:35:6a:b6"}', '{"ip": "192.168.100.123", "mac": " 0:1a:a9:1f:a1:b1"}', '{"ip": "192.168.100.124", "mac": " 0:1a:a9:c4:85:5b"}', '{"ip": "192.168.100.125", "mac": " 0:1a:a9:c4:7f:b"}', '{"ip": "192.168.100.126", "mac": " 0:1a:a9:c4:61:67"}', '{"ip": "192.168.100.127", "mac": " 0:1a:a9:c4:88:97"}', '{"ip": "192.168.100.128", "mac": " 58:69:6c:35:71:a4"}', '{"ip": "192.168.100.131", "mac": " 0:1a:a9:1c:14:59"}', '{"ip": "192.168.100.132", "mac": " 0:1a:a9:1c:3c:59"}', '{"ip": "192.168.100.133", "mac": " 0:1a:a9:1c:1f:99"}', '{"ip": "192.168.100.134", "mac": " 0:1a:a9:1c:10:19"}', '{"ip": "192.168.100.135", "mac": " 0:1a:a9:bc:38:6b"}', '{"ip": "192.168.100.141", "mac": " 0:1a:a9:1f:a1:b5"}', '{"ip": "192.168.100.142", "mac": " 0:1a:a9:1e:d4:15"}', '{"ip": "192.168.100.143", "mac": " 0:1a:a9:46:e6:d6"}', '{"ip": "192.168.100.144", "mac": " 0:1a:a9:46:e7:50"}', '{"ip": "192.168.100.150", "mac": " 58:69:6c:8e:d7:f0"}', '{"ip": "192.168.100.151", "mac": " 58:69:6c:8e:e6:0"}', '{"ip": "192.168.100.152", "mac": " 58:69:6c:8e:e3:60"}', '{"ip": "192.168.100.155", "mac": " 58:69:6c:8e:e3:24"}', '{"ip": "192.168.100.156", "mac": " 58:69:6c:8e:e3:62"}', '{"ip": "192.168.100.157", "mac": " 58:69:6c:8e:e6:5e"}', '{"ip": "192.168.100.201", "mac": " 14:14:4b:1b:91:57"}', '{"ip": "210.45.241.2", "mac": " 0:9:6b:71:a4:be"}', '{"ip": "210.45.241.3", "mac": " 0:90:fb:30:95:6d"}', '{"ip": "210.45.241.4", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.5", "mac": " 0:1e:b:c5:38:3a"}', '{"ip": "210.45.241.6", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.12", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.14", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.16", "mac": " 0:25:90:9d:28:24"}', '{"ip": "210.45.241.25", "mac": " 6c:92:bf:32:c7:fc"}','{"ip": "192.168.100.68", "mac": " 0:0:0:0:0:0"}', '{"ip": "192.168.100.90", "mac": " 0:1a:a9:c5:55:33"}', '{"ip": "192.168.100.91", "mac": " 0:1a:a9:c5:5a:e7"}', '{"ip": "192.168.100.92", "mac": " 0:1a:a9:c5:5b:21"}', '{"ip": "192.168.100.93", "mac": " 0:1a:a9:c5:55:49"}', '{"ip": "192.168.100.94", "mac": " 0:1a:a9:c5:53:d3"}', '{"ip": "192.168.100.95", "mac": " 14:14:4b:19:e2:b"}', '{"ip": "192.168.100.101", "mac": " 14:14:4b:60:44:a5"}', '{"ip": "192.168.100.102", "mac": " 58:69:6c:35:6e:f0"}', '{"ip": "192.168.100.103", "mac": " 58:69:6c:35:70:10"}', '{"ip": "192.168.100.104", "mac": " 58:69:6c:35:6c:c0"}', '{"ip": "192.168.100.105", "mac": " 58:69:6c:35:6f:16"}', '{"ip": "192.168.100.106", "mac": " 58:69:6c:35:6f:58"}', '{"ip": "192.168.100.107", "mac": " 58:69:6c:35:6b:96"}', '{"ip": "192.168.100.108", "mac": " 58:69:6c:35:6a:b6"}', '{"ip": "192.168.100.123", "mac": " 0:1a:a9:1f:a1:b1"}', '{"ip": "192.168.100.124", "mac": " 0:1a:a9:c4:85:5b"}', '{"ip": "192.168.100.125", "mac": " 0:1a:a9:c4:7f:b"}', '{"ip": "192.168.100.126", "mac": " 0:1a:a9:c4:61:67"}', '{"ip": "192.168.100.127", "mac": " 0:1a:a9:c4:88:97"}', '{"ip": "192.168.100.128", "mac": " 58:69:6c:35:71:a4"}', '{"ip": "192.168.100.131", "mac": " 0:1a:a9:1c:14:59"}', '{"ip": "192.168.100.132", "mac": " 0:1a:a9:1c:3c:59"}', '{"ip": "192.168.100.133", "mac": " 0:1a:a9:1c:1f:99"}', '{"ip": "192.168.100.134", "mac": " 0:1a:a9:1c:10:19"}', '{"ip": "192.168.100.135", "mac": " 0:1a:a9:bc:38:6b"}', '{"ip": "192.168.100.141", "mac": " 0:1a:a9:1f:a1:b5"}', '{"ip": "192.168.100.142", "mac": " 0:1a:a9:1e:d4:15"}', '{"ip": "192.168.100.143", "mac": " 0:1a:a9:46:e6:d6"}', '{"ip": "192.168.100.144", "mac": " 0:1a:a9:46:e7:50"}', '{"ip": "192.168.100.150", "mac": " 58:69:6c:8e:d7:f0"}', '{"ip": "192.168.100.151", "mac": " 58:69:6c:8e:e6:0"}', '{"ip": "192.168.100.152", "mac": " 58:69:6c:8e:e3:60"}', '{"ip": "192.168.100.155", "mac": " 58:69:6c:8e:e3:24"}', '{"ip": "192.168.100.156", "mac": " 58:69:6c:8e:e3:62"}', '{"ip": "192.168.100.157", "mac": " 58:69:6c:8e:e6:5e"}', '{"ip": "192.168.100.201", "mac": " 14:14:4b:1b:91:57"}', '{"ip": "210.45.241.2", "mac": " 0:9:6b:71:a4:be"}', '{"ip": "210.45.241.3", "mac": " 0:90:fb:30:95:6d"}', '{"ip": "210.45.241.4", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.5", "mac": " 0:1e:b:c5:38:3a"}', '{"ip": "210.45.241.6", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.12", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.14", "mac": " 0:0:0:0:0:0"}', '{"ip": "210.45.241.16", "mac": " 0:25:90:9d:28:24"}', '{"ip": "210.45.241.25", "mac": " 6c:92:bf:32:c7:fc"}',],
      packIPV4:[],
      packIPV6:[],
      newpackIPV4:{},
      newpackIPV6:{},
      newpack:{},
      totalNumber:0,
      currentData:[],
      prePageSize:40,
      currentPage: 1,
      changed: true,
    }
  },
  methods: {
      // dispose(){
      //   // for(let a=0; a<this.totalNumber)
      // },
      //每页分配多少个数据项
      handleSizeChange(val) {
        // console.log(`每页 ${val} 条`);
        this.prePageSize = val;
        let e = [];
        for(let i=(this.currentPage-1)*val; i<this.currentPage*val; i++){
          e.push(this.newpack[i]);
          }
        // console.log('每页：'+val+'条','当前每页数量'+this.prePageSize,'当前是第'+this.currentPage+'页',e);
        this.currentData = e;
      }, 
      //跳转到第几页，暂时不管这个
      handleCurrentChange(val) {
        // console.log(`当前页: ${val}`);
        let c = [];
        this.currentPage = val;//现在是4
        for(let i = ((val-1)*this.prePageSize); i<val*this.prePageSize; i++){
          c.push(this.newpack[i]);
        }
        this.currentData = c;//现在是不完全的十几个
        console.log('当前每页数量'+this.prePageSize,'当前是第'+this.currentPage+'页',c);
      },
      //马上就解决了，通过初始化ipv4,ipv6数据包，传入newpack，再执行currentData即可完成。
      init(){
        // console.log(this.packIPV6);
        // this.newpackIPV6 = this.packIPV6;
        // console.log('~~~~~~~:',this.packIPV6);
        // this.newpackIPV4 = this.parseData(this.packIPV4);
        // this.newpack = this.newpackIPV4;
        // console.table(this.newpack);
        this.handleSizeChange(40);
      },
      total(pack){
        this.totalNumber = pack.length;
      },
      parseData(pack, newpack){
        // console.log(pack);
        this.total(pack);
        var b=[];
        for(var i=0; i<this.totalNumber; i++){
          // console.log(this.pack.length);
          let a = [JSON.parse(pack[i])];
          // console.log(a);
          b.push(a[0]);
        }
        return b;
      },
      switchdata(){
        if(this.changed){
          this.newpack = this.newpackIPV6;
        }
        else{
          this.newpack = this.newpackIPV4;
        }
        this.currentPage = 1;
        this.handleSizeChange(this.prePageSize);
        // console.log(this.newpack);
        this.total(this.newpack);
        this.changed = !this.changed;
        
      }
    },
  created: function(){
    axios.get('http://210.45.240.117/api/ipv4')
    .then(response=>{
      // console.log(response);
      this.packIPV4 = response;
      let t = response.data;
      t = t.replace(/'/g,"");
      this.newpackIPV4 = JSON.parse(t);
      console.log(this.newpackIPV4);
    })
    .catch(error=>{
      // console.log(error);
      // alert('ipv4网络错误，请稍后再试');
    })
    axios.get('http://210.45.240.117/api/ipv6')
    .then(response=>{
      // console.log(response.data);
      // console.log('===============',);
      let t = response.data;
      t = t.replace(/'/g,"");
      this.newpackIPV6 = JSON.parse(t);
      console.log(this.newpackIPV6);
    })
    .catch(error=>{
      // console.log(error);
      // alert('ipv6网络错误，请稍后再试');
    })
  },
  beforeMount :function(){
    this.init();
  },
  props: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.page-number {
  margin-top:10px;
}
</style>
