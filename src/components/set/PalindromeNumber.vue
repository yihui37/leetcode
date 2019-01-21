<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a
          href="https://leetcode-cn.com/articles/palindrome-number/"
          target="_blank"
        >Palindrome Number</a></h3>
      <section>
        <h4 class="subTitle">No.9 Question:</h4>
        <p>Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.</p>
        <p>
          <b>Example 1:</b>
          <pre><b>Input:</b> 121<br><b>Output:</b> true</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre><b>Input:</b> -121<br><b>Output:</b> false<br><b>Explanation:</b> From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.</pre>
        </p>
        <p>
          <b>Example 3:</b>
          <pre><b>Input:</b> 10<br><b>Output:</b> false<br><b>Explanation:</b> Reads 01 from right to left. Therefore it is not a palindrome.</pre>
        </p>
        <p><b>Follow up:</b></p>
        <p>Coud you solve it without converting the integer to a string?</p>
      </section>
    </article>
    <div class="paramsWrap">
      <h4 class="subTitle">Params</h4>
      <label>Number</label>
      <el-input
        type="text"
        v-model="number"
      ></el-input>
      <p>
        <el-button
          type="primary"
          @click="submit(number)"
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
        label="解法一  22.1% 288ms"
        name="1"
      >
        <h5>我的第一次解法 使用Array.reverse()方法</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  44.21% 260ms"
        name="2"
      >
        <h5>不转为String实现倒序</h5>
        <pre>
        <code>{{answers[2]}}</code>
      </pre>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number: -120,
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(x) {
        let r = x.toString().split("").reverse().join("");
        return r===x.toString();
    };`,
        "2": `
    submit(x) {
        let xReverse = 0, xOrg = x;
        if (xOrg < 0) {
            return false;
        }
        while (x) {
            xReverse = xReverse * 10 + x % 10; 
            x = Math.floor(x/10);
        }
        if (xReverse === xOrg) {
            return true;
        }
        return false;
    }`
      }
    };
  },
  mounted() {},
  methods: {
    changeTab({ name }) {
      this.activeTab = name;
      console.log("changeTab", name, this.activeTab);
    },
    /**
     * @param {number} number
     * @return {number}
     */
    submit(number) {
      const method = this[`method${this.activeTab}`];
      method && method(number);
    },
    /**
     * @param {number} x
     * @return {number}
     */
    method1(x) {
      try {
        let r = x
          .toString()
          .split("")
          .reverse()
          .join("");
        this.result = r === x.toString();
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 数值个十百位数
    method2(x) {
      try {
        let xReverse = 0,
          xOrg = x;
        if (xOrg < 0) return false;
        while (x) {
          // 不转为string，实现倒序
          xReverse = xReverse * 10 + (x % 10);
          x = Math.floor(x / 10);
        }
        this.result = xReverse === xOrg;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    }
    // // hash for循环
    // method3(number) {
    //   try {
    //     const nums = number.split(",").map(num => Number(num));
    //     let hash = {};
    //     for (let i = 0; i < nums.length; i++) {
    //       if (hash[-nums[i]] !== undefined) {
    //         this.result = [hash[-nums[i]], i];
    //         this.execute = "success";
    //         return;
    //       }
    //       hash[nums[i]] = i;
    //       console.log("hash", hash);
    //     }
    //     this.result = [];
    //     this.execute = "error";
    //   } catch (err) {
    //     this.result = err;
    //     this.execute = "error";
    //   }
    // }
  }
};
</script>

<style scoped>
</style>