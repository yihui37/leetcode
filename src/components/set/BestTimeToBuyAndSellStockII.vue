<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a
          href="https://leetcode-cn.com/articles/best-time-to-buy-and-sell-stock-ii/"
          target="_blank"
        >Best Time to Buy and Sell Stock II</a></h3>
      <section>
        <h4 class="subTitle">No.122 Question:</h4>
        <p>Say you have an array for which the ith element is the price of a given stock on day i.</p>
        <p>Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).</p>
        <p>
          <b>Note: </b>
          You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
        </p>
        <p>
          <b>Example 1:</b>
          <pre><b>Input:</b> [7,1,5,3,6,4]<br><b>Output:</b> 7<br><b>Explanation:</b> Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre><b>Input:</b> [1,2,3,4,5]<br><b>Output:</b> 4<br><b>Explanation:</b> Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.<br/>Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.</pre>
        </p>
        <p>
          <b>Example 3:</b>
          <pre><b>Input:</b> [7,6,4,3,1]<br><b>Output:</b> 0<br><b>Explanation:</b> In this case, no transaction is done, i.e. max profit = 0.</pre>
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
        label="解法一  64ms"
        name="1"
      >
        <h5>我的第一次解法</h5>
        <p>将每天的股票值画成折线图，仅计算每个上升段落的最高与最低差值。即多次买卖都是在最低点买入并在最高点卖出。</p>
        <p>具体如下：</p>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  64ms"
        name="2"
      >
        <h5>将上一方法代码精炼一下，不需要再记录每个谷值后的峰值和它们之间的差额。</h5>
        <p>将每天的股票值画成折线图，假设每天都将前一天的卖出并买入当天的，亏本的日子都排除，即计算每天涨的部分和，持续增加从连续交易中获得的利润。</p>
        <p>具体如下：</p>
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
      inputValue: [7, 1, 5, 3, 6, 4],
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(prices) {
        if(!prices.length) return 0;
        let startPrice = prices[0],
            stepProfit = 0,
            result = 0;
        for(let i = 1;i<prices.length;i++){
            if(prices[i] < prices[i-1]){
                result += stepProfit;
                startPrice = prices[i];
                stepProfit = 0;
            }else if(prices[i] > prices[i-1]){
                stepProfit = prices[i] - startPrice;
            }
        }
        result += stepProfit;   // 加上最后一次的利润
        return result;
    };`,
        "2": `
    submit(prices) {
        if(!prices.length) return 0;
        let result = 0;
        for(let i = 1;i<prices.length;i++){
            if(prices[i] > prices[i-1]){
                result += prices[i] - prices[i-1];
            }
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
      method && method(this.inputValue);
    },
    /**
     * @param {number[]} prices
     * @return {number}
     */
    // 想一下折线图，仅计算上涨段落和
    method1(prices) {
      try {
        if (!prices.length) return 0;
        let startPrice = prices[0],
          stepProfit = 0,
          result = 0;
        for (let i = 1; i < prices.length; i++) {
          if (prices[i] < prices[i - 1]) {
            result += stepProfit;
            startPrice = prices[i];
            stepProfit = 0;
          } else if (prices[i] > prices[i - 1]) {
            stepProfit = prices[i] - startPrice;
          }
        }
        result += stepProfit; // 加上最后一次的利润
        this.result = result;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 解法精炼一下，假设从不亏本，计算买完就涨的所有情况
    method2(prices) {
      try {
        if (!prices.length) return 0;
        let result = 0;
        for (let i = 1; i < prices.length; i++) {
          if (prices[i] > prices[i - 1]) {
            result += prices[i] - prices[i - 1];
          }
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