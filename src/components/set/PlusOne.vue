<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Plus One</a></h3>
      <section>
        <h4 class="subTitle">No.66 Question:</h4>
        <p>Given a non-empty array of digits representing a non-negative integer, plus one to the integer.</p>
        <p>The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.</p>
        <p>You may assume the integer does not contain any leading zero, except the number 0 itself.</p>
        <p>
          <b>Example 1:</b>
          <pre>Input: [1,2,3]<br>Output: [1,2,3]<br>Explanation: The array represents the integer 123.</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Input: [4,3,2,1]<br>Output: [4,3,2,2]<br>Explanation: The array represents the integer 4321.</pre>
        </p>
      </section>
    </article>
    <div class="paramsWrap">
      <h4 class="subTitle">Params</h4>
      <label>InputValue</label>
      <el-input
        type="text"
        v-model="inputValue"
      ></el-input>
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
        label="解法一"
        name="1"
      >
        <h5>我的第一次解法 arr.join -> string -> number+1 -> string -> split -> arr[nums]。具体如下：</h5>
        <el-tag type="danger">错误：未考虑到数值的有效范围，超出后不可使用数学加法完成</el-tag>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  72ms"
        name="2"
      >
        <h5>从数组最后一个元素开始+1，如果和为10，则对前一个元素继续加1，否则结束循环。注意第一位数结果进1，使用unshift向数组开头添加1。</h5>
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
      inputValue: "9",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(digits) {
        var num = parseInt(digits.join('')) + 1;
        return num.toString().split('').map(char=>Number(char));
    };`,
        "2": `
    submit(digits) {
        for(let i = digits.length - 1;i>-1;i--){
            let num = digits[i] + 1;
            if(num == 10) {
                digits[i] = 0;
                if(i==0){
                    // 第一位满10进1，多一位
                    digits.unshift(1);
                }
            }else{
                digits[i] = num;
                break;
            }
        }
        return digits;
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
      method && method(this.inputValue.split(",").map(char => Number(char)));
    },
    /**
     * @param {array} digits
     * @return {String}
     */
    // 数学加法
    method1(digits) {
      try {
        let str = digits.join(""),
          num = Number(str) + 1,
          res = String(num)
            .split("")
            .map(item => Number(item));
        this.result = res;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 从最后一个元素开始单个加1，逢十进一
    method2(digits) {
      try {
        for (let i = digits.length - 1; i > -1; i--) {
          let num = digits[i] + 1;
          if (num == 10) {
            digits[i] = 0;
            if (i == 0) {
              // 第一位满10进1，多一位
              debugger;
              digits.unshift(1);
            }
          } else {
            digits[i] = num;
            break;
          }
        }
        this.result = digits.join(",");
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