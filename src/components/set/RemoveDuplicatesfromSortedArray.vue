<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a
          href="https://leetcode-cn.com/articles/remove-duplicates-from-sorted-array/"
          target="_blank"
        >Remove Duplicates from Sorted Array</a></h3>
      <section>
        <h4 class="subTitle">No.26 Question:</h4>
        <p>Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.</p>
        <p>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.</p>
        <p>
          <b>Example 1:</b>
          <pre>Given nums = [1,1,2]<br>Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.<br>It doesn't matter what you leave beyond the returned length.</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Given nums = [0,0,1,1,1,2,2,3,3,4]<br>Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.<br>It doesn't matter what values are set beyond the returned length.</pre>
        </p>
        <p><b>Clarification::</b></p>
        <p>Confused why the returned value is an integer but your answer is an array?<br>
          Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.
          <br>Internally you can think of this:
          <pre>// nums is passed in by reference. (i.e., without making a copy)<br>int len = removeDuplicates(nums);<br><br>// any modification to nums in your function would be known by the caller.<br>// using the length returned by your function, it prints the first len elements.<br>for (int i = 0; i &lt; len; i++) {<br>  print(nums[i]);<br>}
        </pre>
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
        label="解法一  96ms"
        name="1"
      >
        <h5>我的第一次解法 第一次解想了很久没有想出来，后来看了一下题目关联的标签为TwoPointers，由此启发想到使用双指针来解决：用一个指针来遍历所有元素，另一指针来存储不重复元素（替换原数组），具体如下：</h5>
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
      inputValue: "0,1,1,2,3,3,3,4,4",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(nums) {
        const len = nums.length;
        let j = 0;
        for(let i = 0;i<len;i++){
            if(nums[i]!==nums[j]) nums[++j] = nums[i];
        }
        return j+1;
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
    /**
     * @param {number} number
     * @return {number}
     */
    submit() {
      const method = this[`method${this.activeTab}`];
      method && method(this.inputValue.split(","));
    },
    /**
     * @param {array} nums
     * @return {String}
     */
    //正则 从0到all匹配
    method1(nums) {
      try {
        const len = nums.length;
        if (!len) {
          this.result = "[]";
          this.execute = "success";
          return;
        }
        let j = 0;
        for (let i = 0; i < len; i++) {
          if (nums[i] !== nums[j]) nums[++j] = nums[i]; // 题干中说nums是一个有序数组，
          // 因此只需要比较最后一个不重复项与当前项的大小即可
          // 不必考虑会不会与前面的元素重复
        }
        nums.length = j + 1;
        this.result = `[${nums.join(",")}]`;
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