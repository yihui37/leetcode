<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Maximum Subarray</a></h3>
      <section>
        <h4 class="subTitle">No.53 Question:</h4>
        <p>Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.</p>
        <p>Given an integer n where 1 ≤ n ≤ 30, generate the n^th term of the count-and-say sequence.</p>
        <p>
          <b>Example:</b>
          <pre>Input: [-2,1,-3,4,-1,2,1,-5,4],<br>Output: 6<br>Explanation: [4,-1,2,1] has the largest sum = 6.</pre>
        </p>
        <p><b>Follow up:</b><br>If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.</p>
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
        label="解法一  Time Limit Exceeded"
        name="1"
      >
        <h5>我的第一次解法 第一反应就是从前到后循环遍历所有可能性组合，从所有结果中取最大值，但是提交的时候提示我Time Limit Exceeded了。这个费时费力的笨方法直接证明了学算法的重要性/(ㄒoㄒ)/~~。具体如下：</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  80ms 动态规划"
        name="2"
      >
        <h5>看提示有动态规划，因此想到在遍历过程中，可以把问题看成是求每一个从0到i的数组中最大的子序列数组和，如果前一次遍历最大和为负数，相当于做减法，因此直接返回当前元素，否则相加。具体如下：</h5>
        <pre>
        <code>{{answers[2]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法三  76ms 动态规划 优化"
        name="3"
      >
        <h5>搜索了一下动态规划，总结解法二有如下递归公式：dp_n = dp_n-1 > 0 ? dp_n-1 + array[n] : array[n]。具体如下：</h5>
        <pre>
        <code>{{answers[3]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法四  80ms 分治算法"
        name="4"
      >
        <h5>题干说明还可以使用分治算法来解决，由于对此不了解，因此直接百度了答案，才知道原来二分法也是分治算法的一种。具体如下：</h5>
        <pre>
        <code>{{answers[4]}}</code>
      </pre>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: "-2,1,-3,4,-1,2,1,-5,4",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    var maxSubArray = function(nums) {
        let len = nums.length,sum = nums[0];
        const getMaxSum = (arr)=>{
            let len = arr.length,
                sum = arr[0];
            for(let i = 1;i<=len;i++){
                let tsum = 0;
                for(let j = 0;j<i;j++){
                    tsum += arr[j];
                }
                if(sum<tsum) sum = tsum;
            }
            return sum;
        };
        
        for(let i = 0;i<len;i++){
            let arr = nums.slice(i),
                tsum = getMaxSum(arr);
            if(sum < tsum) sum = tsum;
        }
        return sum;
    };`,
        "2":`
    var maxSubArray = function(nums) {
        let res = nums[0],
            sum = 0;
        for (let num of nums) {
            if (sum > 0)
                sum += num;
            else
                sum = num;
            res = Math.max(res, sum);
        }
        return res;
    };`,
        "3":`
    var maxSubArray = function(nums) {
        let max = nums[0],
            dp_n = nums[0];
        for(let i=1; i<nums.length; i++){
            dp_n = nums[i] + (dp_n>0 ? dp_n : 0);
            max = dp_n>max ? dp_n : max;
        }
        return max;
    };`,
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
      method && method(this.inputValue.split(',').map(num=>Number(num)));
    },
    /**
     * @param {array} nums
     * @return {number}
     */
    // 遍历所有可能情况
    method1() {
        this.result = "Time Limit Exceeded";
        this.execute = "error";
    },
    // 动态规划
    method2(nums) {
      try {
        let res = nums[0],
            sum = 0;
        for (let num of nums) {
            if (sum > 0)
                sum += num;
            else
                sum = num;
            res = Math.max(res, sum);
        }
        this.result = res;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 动态规划  公式
    method3(nums) {
      try {
        let max = nums[0],
        dp_n = nums[0];
        for(let i=1; i<nums.length; i++){
            dp_n = nums[i] + (dp_n>0 ? dp_n : 0);
            max = dp_n>max ? dp_n : max;
        }
        this.result = max;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 分治算法  todo
    method4(nums) {
      try {
        let max = nums[0],
        dp_n = nums[0];
        for(let i=1; i<nums.length; i++){
            dp_n = nums[i] + (dp_n>0 ? dp_n : 0);
            max = dp_n>max ? dp_n : max;
        }
        this.result = max;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
  }
};
</script>

<style scoped>
</style>