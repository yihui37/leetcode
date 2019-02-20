<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Sqrt(x)</a></h3>
      <section>
        <h4 class="subTitle">No.69 Question:</h4>
        <p>Implement int sqrt(int x).</p>
        <p>Compute and return the square root of x, where x is guaranteed to be a non-negative integer.</p>
        <p>Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.</p>
        <p>
          <b>Example 1:</b>
          <pre>Input: 4<br>Output: 2<br></pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Input: 8<br>Output: 2<br>Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.</pre>
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
        label="解法一  92ms"
        name="1"
      >
        <h5>我的第一次解法 一开始想直接使用JS中sqrt方法，然后看了一下题意是自己实现这种方法，看了题干下的提示想到了使用二分法，逐渐逼近的方式。
          即在[0, n/2+1]这个范围内进行二分搜索，求出n的平方根。具体如下：</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  96ms 牛顿迭代法"
        name="2"
      >
        <h5>在网上看到了另一个解法，采用的是牛顿迭代法。本题中：计算x^2 = n的解，令f(x)=x^2-n，相当于求解f(x)=0的解，推导出的最后公式为：xi+1=xi - (xi2 - n) / (2xi) = xi - xi / 2 + n / (2xi) = xi / 2 + n / 2xi = (xi + n/xi) / 2。具体如下</h5>
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
      inputValue: 6,
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(x) {
        if (x <= 1) return x;
        let left = 0,
            right =parseInt(x/2+1);
        while(left < right){
            let mid = parseInt((left+right) / 2),
                num = mid * mid;
            if (num > x) {
                right = mid;
            }else{
                left = mid + 1;
            }
        }
        return right -1;
    };`,
        "2": `
    submit(x) {
        if (x == 0) return 0;
        let last = 0,
            res = 1;
        while (res != last)
        {
            last = res;
            res = (res + x / res) / 2;
        }
        return parseInt(res);
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
      method && method(this.inputValue);
    },
    /**
     * @param {array} digits
     * @return {String}
     */
    // 二分法
    method1(x) {
      try {
        if (x <= 1) return x;
        let left = 0,
          right = parseInt(x / 2 + 1);
        while (left < right) {
          let mid = parseInt((left + right) / 2),
            num = mid * mid;
          if (num > x) {
            right = mid;
          } else {
            left = mid + 1;
          }
        }
        this.result = right - 1;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 牛顿迭代法
    method2(x) {
      try {
        if (x == 0) return 0;
        let last = 0,
          res = 1;
        while (res != last) {
          last = res;
          res = (res + x / res) / 2;
        }
        this.result = parseInt(res);
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