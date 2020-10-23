<template>
  <div id="wrapper">
    <div class="file">
      <div class="assets">
           <img  style="height:100px; width: auto;;" src="~@/assets/dy.png" alt="electron-vue" />
           <div class="title">vue的assets下图片</div>
      </div>
      <div class="static">
            <img v-bind:src="imageUrl" style="height:100px; width: auto;;">
            <div class="title">static下图片</div>
      </div>
    </div>
   
    <main>
      <div class="left-side">
        <span >
          合成成功：
        </span>
        <system-information></system-information>
      </div>
      <div class="nale ">
        <div class="title">sqlite3数据库的数据</div>
        <template v-for="(item, i) in list">
          <div :key="i">姓名：{{ item.name }}</div>
        </template>
      </div>
      <div class="right-side">
        
      </div>
    </main>
  </div>
</template>

<script>
import SystemInformation from "./LandingPage/SystemInformation";
import fs from "fs";
import path from "path";
import { remote } from "electron";
export default {
  name: "landingpage",
  components: { SystemInformation },
  data() {
    return {
      list: [],
      // 注意 路径的起始是 `static/`
      imageUrl: 'static/imgs/static.png' 
    };
  },
  created() {
    let _that = this;
    const sqlite3 = require("sqlite3").verbose();
    const path = require("path");
    console.log("路径：",__resources)
    const db = new sqlite3.Database(path.join(__resources, "/local.db"));
      db.run("create table test( id INTEGER PRIMARY KEY AUTOINCREMENT,name varchar(15))", function() {
      let addname="测名称："+_that.datet();
      db.run('insert into test (name) values("'+addname+'")', function() {
        db.all("select * from test order by id desc limit 8 ", function(err, res) {
          if (!err) {
            _that.list=res
            console.log(JSON.stringify(res));
          } else {
            console.log(err);
          }
        });
      });
    });
    //静态文件
    // let fileContents = fs.readFileSync(path.join(__static, '/someFile.txt'), 'utf8')
    // console.log("文件:",fileContents)
    // let fileContents = fs.readFileSync(path.join(__static, '/someFile.txt'), 'utf8')
    //  console.log("静态文件:",fileContents)

  },
  methods: {
    open(link) {
      this.$electron.shell.openExternal(link);
    },
    datet(){
       const date = new Date();
      const Y = date.getFullYear() + '-';
      const M = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
      const D = date.getDate() + ' ';
      const h = date.getHours() + ':';
      const m = date.getMinutes();
      const dateString = Y + M + D + h + m;
      return dateString;
    }
  },
};
</script>
<style lang="scss" scoped>
 .file{
   display: flex;
   .assets{
     flex:1;
   }
   .static{
      flex:1; 
   }
 }
</style>
<style >
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Source Sans Pro", sans-serif;
}

#wrapper {
  background: radial-gradient(
    ellipse at top left,
    rgba(255, 255, 255, 1) 40%,
    rgba(229, 229, 229, 0.9) 100%
  );
  height: 100vh;
  padding: 60px 80px;
  width: 100vw;
}

#logo {
  height: auto;
  margin-bottom: 20px;
  width: 420px;
}

main {
  display: flex;
  justify-content: space-between;
}

main > div {
  flex-basis: 50%;
}

.left-side {
  display: flex;
  flex-direction: column;
}

.welcome {
  color: #555;
  font-size: 23px;
  margin-bottom: 10px;
}

.title {
  color: #2c3e50;
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 6px;
}

.title.alt {
  font-size: 18px;
  margin-bottom: 10px;
}

.doc p {
  color: black;
  margin-bottom: 10px;
}

.doc button {
  font-size: 0.8em;
  cursor: pointer;
  outline: none;
  padding: 0.75em 2em;
  border-radius: 2em;
  display: inline-block;
  color: #fff;
  background-color: #4fc08d;
  transition: all 0.15s ease;
  box-sizing: border-box;
  border: 1px solid #4fc08d;
}

.doc button.alt {
  color: #42b983;
  background-color: transparent;
}
</style>
