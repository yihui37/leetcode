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
        label="解法一  72ms"
        name="1"
      >
        <h5>我的第一次解法 arr.join -> string -> number+1 -> string -> split -> arr[nums]。具体如下：</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <!-- <el-tab-pane
        label="解法二  44.32% 72ms"
        name="2"
      >
        <h5>使用.startsWith(String prefix, int toffset)方法代替正则匹配，使用第一个元素作为校验值，不匹配则依次去掉元素的最后一个字符继续匹配，直到匹配到全部符合的prefix</h5>
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
      inputValue: 6,
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    let getNext = function(str) {
      let strArr = str.split("").map(char => Number(char)),
        count = 0,
        curVal = strArr[0],
        res = "";
      for (let i = 0; i < strArr.length; i++) {
        if (curVal == strArr[i]) {
          count++;
        } else {
          res += String(count)+String(curVal);
          count = 1;
          curVal = strArr[i];
        }
      }
      res += String(count)+String(curVal);
      return res;
    };

    submit(n) {
        let result = "1";
        for (let j = 1; j < n; j++) {
          result = getNext(result);
        }
        return result;
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
      method && method(this.inputValue.split(','));
    },
    /**
     * @param {array} digits
     * @return {String}
     */
    //正则 从0到all匹配
    method1(digits) {
      try {
        let str = digits.join(''),
        num = Number(str)+1,
        res = String(num).split('').map(item=>Number(item))

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