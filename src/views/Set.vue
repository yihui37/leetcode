
 <template>
  <div class="setWrap">
    <h1>LeetCode习题集{{this.$route.params.id}}</h1>
    <el-collapse accordion v-model="activeName">
      <el-collapse-item name="1">
        <template slot="title">
          Two Sum
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <TwoSum></TwoSum>
      </el-collapse-item>
    </el-collapse>
    <el-button
      v-if="activeName"
      class="toggleBtn el-icon-arrow-up"
      type="warning"
      size="small"
      @click="activeName=''"
    >&nbsp;收起</el-button>
  </div>
</template>
 
 <script>
import TwoSum from "../components/set/TwoSum.vue";
export default {
  components: {
    TwoSum
  },
  watch: {
    "$route.params": {
      handler(newValue) {
        if (newValue.id) {
          this.activeName = String(newValue.id);
          return;
        } else {
          this.$router.push({ path: "/set/1" });
        }
      },
      immediate: true,
      deep: true
    }
  },
  data() {
    return {
      activeName: "1"
    };
  },
  methods: {
    name() {}
  }
};
</script>
 
 <style lang="scss">
.header-icon {
  margin-left: 15px;
}
.el-collapse-item__wrap {
  background-color: #d1e4f7;
  padding: 10px;
}
.toggleBtn {
  position: fixed;
  right: 10px;
  bottom: 20px;
}
.exerciseItemWrap {
  text-align: left;
  .mainTitle {
    text-align: center;
  }
  pre {
    padding: 10px;
    min-height: 30px;
    background-color: #ecf5ff;
    border-left: 3px solid #333;
    &.success {
      border-color: #67c23a;
    }
    &.error {
      border-color: #f56c6c;
    }
  }
}
</style>