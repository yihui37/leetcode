<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Count and Say</a></h3>
      <section>
        <h4 class="subTitle">No.38 Question:</h4>
        <p>The count-and-say sequence is the sequence of integers with the first five terms as following:
          <ul>
            <li>1. 1</li>
            <li>2. 11</li>
            <li>3. 21</li>
            <li>4. 1211</li>
            <li>5. 111221</li>
          </ul>
          1 is read off as "one 1" or 11.<br>11 is read off as "two 1s" or 21.<br>21 is read off as "one 2, then one 1" or 1211.
        </p>
        <p>Given an integer n where 1 ≤ n ≤ 30, generate the n^th term of the count-and-say sequence.</p>
        <p>Note: Each term of the sequence of integers will be represented as a string.</p>
        <p>
          <b>Example 1:</b>
          <pre>Input: 1<br>Output: "1"</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Input: 4<br>Output: "1211"</pre>
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
        <h5>我的第一次解法 借助了题目的提示1，才看懂了题目的意思，是用连续重复数字的个数和值组成下一个数，例如'111221'读为'3个1，2个2，1个1'，因此下一个数为'312211'。由此的思路为，根据传入值，从第一个‘1’开始循环求下一个数，写一个公共的求下一个数的方法，把上一个数作为参数传入即可。公共方法中，循环当前字符串中每一个字符，记录联系相同字符的个数个值并记录拼接返回。具体如下：</h5>
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
      method && method(Number(this.inputValue));
    },
    /**
     * @param {number} n
     * @return {String}
     */
    //正则 从0到all匹配
    method1(n) {
      try {
        let getNext = function(str) {
          let strArr = str.split("").map(char => Number(char)),
            count = 0,
            curVal = strArr[0],
            res = "";
          for (let i = 0; i < strArr.length; i++) {
            if (curVal == strArr[i]) {
              count++;
            } else {
              res += `${count}${curVal}`;
              count = 1;
              curVal = strArr[i];
            }
          }
          res += `${count}${curVal}`;
          return res;
        };

        let result = "1";
        for (let j = 1; j < n; j++) {
          result = getNext(result);
        }
        this.result = result;
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