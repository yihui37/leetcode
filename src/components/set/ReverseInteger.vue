<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle">Reverse Integer</h3>
      <section>
        <h4 class="subTitle">No.7 Question:</h4>
        <p>Given a <b>32-bit signed integer</b>, reverse digits of an integer.</p>
        <p>
          <b>Example 1:</b>
          <pre>Input: 123<br>Output: 321</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Input: -123<br>Output: -321</pre>
        </p>
        <p>
          <b>Example 3:</b>
          <pre>Input: 120<br>Output: 21</pre>
        </p>
        <p><b>Note:</b></p>
        <p>Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.</p>
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
        label="解法一  31.72% 96ms"
        name="1"
      >
        <h5>我的第一次解法 使用Array.reverse()方法</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  35.76% 92ms"
        name="2"
      >
        <h5>始终数值，个十百位数倒序相加</h5>
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
      let sign = x > 0 ? 1 : -1; // 正负号
      let num = Math.abs(x); // 绝对值
      let reverse = Number(num.toString().split('').reverse().join('')) * sign; // 倒序转换
      if(reverse>Math.pow(2,31)-1 || reverse < Math.pow(-2,31)  ) reverse = 0; // 判断32位数值区间
      return reverse;
    }`,
        "2": `
    submit(x) {
        let r = 0;
        while (x) {
            r = r*10 + x % 10;            
            x = parseInt(x/10);
        }
        if (r > Math.pow(2, 31) - 1 || r <  Math.pow(-2, 31)) {
            return 0;
        }
        return r;
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
        let sign = x > 0 ? 1 : -1; // 正负号
        let num = Math.abs(x); // 绝对值
        let reverse =
          Number(
            num
              .toString()
              .split("")
              .reverse()
              .join("")
          ) * sign; // 倒序转换
        if (reverse > Math.pow(2, 31) - 1 || reverse < Math.pow(-2, 31))
          reverse = 0; // 判断32位数值区间
        this.result = reverse;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 数值个十百位数
    method2(x) {
      try {
        let r = 0;
        while (x) {
          r = r * 10 + (x % 10);
          x = parseInt(x / 10);
        }
        if (r > Math.pow(2, 31) - 1 || r < Math.pow(-2, 31)) {
          this.result = 0;
        } else {
          this.result = r;
        }
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