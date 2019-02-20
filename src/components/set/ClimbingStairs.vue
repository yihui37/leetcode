<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Climbing Stairs</a></h3>
      <section>
        <h4 class="subTitle">No.70 Question:</h4>
        <p>You are climbing a stair case. It takes n steps to reach to the top.</p>
        <p>Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?</p>
        <p><b>Note: </b>Given n will be a positive integer.</p>
        <p>
          <b>Example 1:</b>
          <pre>Input: 2<br>Output: 2<br>Explanation: There are two ways to climb to the top.<br>1. 1 step + 1 step<br>2. 2 steps</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Input: 3<br>Output: 3<br>Explanation: There are three ways to climb to the top.<br>1. 1 step + 1 step + 1 step<br>2. 1 step + 2 steps<br>3. 2 steps + 1 step</pre>
        </p>
      </section>
    </article>
    <div class="paramsWrap">
      <h4 class="subTitle">Params</h4>
      <label>InputValue</label>
      <!-- <el-input
        type="text"
        v-model="inputValue"
      ></el-input> -->
      <pre>{{inputValue}}</pre>
      <p>
        <el-button
          type="primary"
          @click="submit"
        >submit</el-button>
      </p>
    </div>
    <div class="anserWrap">
      <h4 class="subTitle">Result: {{execute}}</h4>
      <pre :class="execute">{{result}}</pre>
    </div>
    <el-tabs
      type="border-card"
      :value="activeTab"
      @tab-click="changeTab"
    >
      <h4 class="subTitle">Answers:</h4>
      <el-tab-pane
        label="解法一  68ms"
        name="1"
      >
        <h5>我的第一次解法</h5>
        <p>一开始觉得题目很熟悉，但是似懂非懂的完全没有头绪，后来看了提示是<b>动态规划</b>类的题目，知道是要根据记住以往的结果来推算演进，但是还是没有想到具体的解决思路。后来在网上的解答中，看到了本题的关键点：<b>到达台阶i的最后一步，只存在两种方法——从i-1台阶迈一步，或者从i-2台阶迈两步</b>，茅塞顿开，想到了具体的解决方法，如下：</p>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <!-- <el-tab-pane
        label="解法二  72ms"
        name="2"
      >
        <h5>从数组最后一个元素开始+1，如果和为10，则对前一个元素继续加1，否则结束循环。注意第一位数结果进1，使用unshift向数组开头添加1。</h5>
        <pre>
        <code>{{answers[2]}}</code>
      </pre>
      </el-tab-pane> -->
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: 3,
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(n) {
        if (n <= 1) return 1;
        let one_forward = 1,
          two_forward = 1,
          res = 0;
        for (let i = 2; i <= n; i++) {
          // res(i) = res(i-1) + res(i-2);
          res = one_forward + two_forward;  // res(i)
          two_forward = one_forward;        // res(i-2)
          one_forward = res;                // res(i-1)
        }
        return res;
    };`
      }
    };
  },
  mounted() {},
  methods: {
    changeTab({ name }) {
      this.activeTab = name;
      this.result = "";
      this.execute = "";
      console.log("changeTab", name, this.activeTab);
    },
    submit() {
      const method = this[`method${this.activeTab}`];
      method && method(parseInt(this.inputValue));
    },
    /**
     * @param {number} n
     * @return {number}
     */
    // Fibonacci数列 动态规划
    method1(n) {
      try {
        if (n <= 1) return 1;
        let one_forward = 1,
          two_forward = 1,
          res = 0;
        for (let i = 2; i <= n; i++) {
          // res(i) = res(i-1) + res(i-2);
          res = one_forward + two_forward; // res(i)
          two_forward = one_forward; // res(i-2)
          one_forward = res; // res(i-1)
        }
        this.result = res;
        this.execute = "success";
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