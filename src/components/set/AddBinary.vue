<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Add Binary</a></h3>
      <section>
        <h4 class="subTitle">No.67 Question:</h4>
        <p>Given two binary strings, return their sum (also a binary string).</p>
        <p>The input strings are both non-empty and contains only characters 1 or 0.</p>
        <p>
          <b>Example 1:</b>
          <pre>Input: a = "11", b = "1"<br>Output: "100"<br></pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Input: a = "1010", b = "1011"<br>Output: "10101"<br></pre>
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
        label="解法一  88ms"
        name="1"
      >
        <h5>我的第一次解法 取a、b中长度较大值作为遍历次数，一次从后到前将每个元素值相加，与2比较大小，满2进1，余数作为当前指针对应元素存入结果集。具体如下：</h5>
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
      inputValue: { a: "1010", b: "1011" },
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(a,b) {
        let aArr = a.split("").map(char=>Number(char)),
            bArr = b.split("").map(char=>Number(char)),
            aLen = aArr.length,
            bLen = bArr.length,
            maxLen = Math.max(aLen,bLen),
            num = 0,
            res = [];
        for(let i = 0;i<maxLen;i++){
            let sum = (aArr[aLen -1 - i] || 0) + (bArr[bLen -1 - i] || 0) + num;
            res[maxLen - 1 - i] = sum > 1 ? sum%2 : sum;
            num = sum > 1 ? Math.floor(sum/2) : 0;
            if(i == maxLen - 1 && num > 0) res.unshift(num);
        }
        return res.join('');
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
    // 数学加法
    method1({ a, b }) {
      try {
        let aArr = a.split("").map(char => Number(char)),
          bArr = b.split("").map(char => Number(char)),
          aLen = aArr.length,
          bLen = bArr.length,
          maxLen = Math.max(aLen, bLen),
          num = 0,
          res = [];
        for (let i = 0; i < maxLen; i++) {
          let sum = (aArr[aLen - 1 - i] || 0) + (bArr[bLen - 1 - i] || 0) + num;
          res[maxLen - 1 - i] = sum > 1 ? sum % 2 : sum;
          num = sum > 1 ? Math.floor(sum / 2) : 0;
          if (i == maxLen - 1 && num > 0) res.unshift(num);
        }

        this.result = res.join("");
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