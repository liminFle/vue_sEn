<template>

  <div id="index">
    <el-container>
      <el-header class="header" style="height:80px;">
      <Headnav></Headnav>
      </el-header>
    </el-container>

    <el-container>
      <el-aside class="aside">
         <Leftnav></Leftnav>
        </el-aside>
        <!-- 使用动态的 transition name -->
          <transition :name="transitionName">
        <keep-alive>
        <el-main>
          <Mainnav/>       
          <router-view/> 
        </el-main> 
        </keep-alive>
        </transition>
    </el-container>

      <el-container>
        <el-footer class="footer">
          <Footer></Footer>
        </el-footer>    
    </el-container>  
  </div>
</template>

<style scoped>
.header {
  background: rgb(84, 92, 100);
}
.aside {
  width: 200px;
}
.footer {
  background: rgb(84, 92, 100);
}
</style>


<script>
import Content from "./Test_api";
import Leftnav from "./navmenu/leftnav";
import Mainnav from "./navmenu/mainnav";
import Headnav from "./navmenu/headnav";
import Footer from "./navmenu/footer";
export default {
  data() {
    return {
      transitionName: 'slide-left'
    };
  },
  components: {
    Content,
    Leftnav,
    Mainnav,
    Headnav,
    Footer
  }, // watch $route 决定使用哪种过渡
  watch: {
    $route(to, from) {
      const toDepth = to.path.split("/").length;
      const fromDepth = from.path.split("/").length;
      this.transitionName = toDepth < fromDepth ? "slide-right" : "slide-left";
    }
  }
};
</script>
