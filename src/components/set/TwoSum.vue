<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle">Two Sum</h3>
      <section>
        <h4 class="subTitle">No.1 Question:</h4>
        <p>Given an array of integers, return indices of the two numbers such that they add up to a specific target.
          <br>You may assume that each input would have exactly one solution, and you may not use the same element twice.
        </p>
        <p>
          <b>Example:</b>
        </p>
        <pre>Given nums = [2, 7, 11, 15], target = 9,<br>Because nums[0] + nums[1] = 2 + 7 = 9,<br>return [0, 1].</pre>
      </section>
    </article>
    <div class="paramsWrap">
      <h4 class="subTitle">Params</h4>
      <label>Array</label>
      <el-input type="text" v-model="array"></el-input>
      <label>Target</label>
      <el-input type="text" v-model="target"></el-input>
      <p>
        <el-button type="primary" @click="submit(array,target)">submit</el-button>
      </p>
    </div>
    <div class="resultWrap">
      <h4 class="subTitle">Result: {{execute}}</h4>
      <pre :class="execute">{{result}}</pre>
    </div>
    <div class="answerWrap">
      <h4 class="subTitle">Answers:</h4>
      <el-tabs type="border-card" :value="activeTab">
        <el-tab-pane label="解法一  2.5% 1025ms" name="1">
          <h5>我的第一次解法 for循环遍历</h5>
          <pre>
            <code>{{answers[1]}}</code>
          </pre>
        </el-tab-pane>

        <el-tab-pane label="解法二  59.88% 80ms" name="2">
          <h5>Hash解法</h5>
          <pre>
            <code>{{answers[2]}}</code>
          </pre>
        </el-tab-pane>
        <el-tab-pane label="解法三  69.95% 72ms" name="3">
          <h5>Hash解法，for循环</h5>
          <pre>
            <code>{{answers[3]}}</code>
          </pre>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      target: "3",
      array: "1,2,3,4,5",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(array, target) {
      const nums = array.split(",").map(num => Number(num));
      for (let [findex, i] of nums.entries()) {
        for (let [sindex,j] of nums.slice(findex + 1).entries()) {
          if (Number(target) == i + j) {
            return [findex, sindex + findex + 1];
          }
        }
      }
    }`,
        "2": `
    submit(array, target) {
      let hash = {};
      for (let [index, value] of nums.entries()) {
        if (hash[target - value] !== undefined) {
          return [hash[target - value], index];
        }
        hash[value] = index;
      }
    }`,
        "3": `
    submit(array, target) {
      let hash = {};
      for (let i = 0; i < nums.length; i++) {
        if (hash[target - nums[i]] !== undefined) {
          return [hash[target - nums[i]], i];
        }
        hash[nums[i]] = i;
      }
    }`
      }
    };
  },
  mounted() {},
  methods: {
    /**
     * @param {string} array
     * @param {number} target
     * @return {number[]}
     */
    submit(array, target) {
      const method = this[`method${this.activeTab}`];
      method && method(array, target);
    },
    /**
     * @param {string} array
     * @param {number} target
     * @return {number[]}
     */
    method1(array, target) {
      try {
        const nums = array.split(",").map(num => Number(num));
        for (let [findex, i] of nums.entries()) {
          for (let [sindex, j] of nums.slice(findex + 1).entries()) {
            if (Number(target) == i + j) {
              this.result = [findex, sindex + findex + 1];
              this.execute = "success";
              return;
            }
          }
        }
        this.result = [];
        this.execute = "error";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // hash  arr.entries()
    method2(array, target) {
      try {
        const nums = array.split(",").map(num => Number(num));
        let hash = {};
        for (let [index, value] of nums.entries()) {
          if (hash[target - value] !== undefined) {
            this.result = [hash[target - value], index];
            this.execute = "success";
            return;
          }
          hash[value] = index;
          console.log("hash", hash);
        }
        this.result = [];
        this.execute = "error";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // hash for循环
    method3(array, target) {
      try {
        const nums = array.split(",").map(num => Number(num));
        let hash = {};
        for (let i = 0; i < nums.length; i++) {
          if (hash[target - nums[i]] !== undefined) {
            this.result = [hash[target - nums[i]], i];
            this.execute = "success";
            return;
          }
          hash[nums[i]] = i;
          console.log("hash2", hash);
        }
        this.result = [];
        this.execute = "error";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    }
  }
};
</script>

<style scoped>
</style>