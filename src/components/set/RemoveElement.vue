<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a
          href="https://leetcode-cn.com/articles/remove-element/"
          target="_blank"
        >Remove Element</a></h3>
      <section>
        <h4 class="subTitle">No.27 Question:</h4>
        <p>Given an array nums and a value val, remove all instances of that value in-place and return the new length.</p>
        <p>Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.</p>
        <p>The order of elements can be changed. It doesn't matter what you leave beyond the new length.</p>
        <p>
          <b>Example 1:</b>
          <pre>Given nums = [3,2,2,3], val = 3,<br>Your function should return length = 2, with the first two elements of nums being 2.<br>It doesn't matter what you leave beyond the returned length.</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre>Given nums = [0,1,2,2,3,0,4,2], val = 2,<br>Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.<br>Note that the order of those five elements can be arbitrary.<br>It doesn't matter what values are set beyond the returned length.</pre>
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
        label="解法一  72ms"
        name="1"
      >
        <h5>我的第一次解法 这道题与26题思路基本一样，双指针，就不多说了，具体如下：</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  76ms"
        name="2"
      >
        <h5>注意到题干中有提示说"The order of elements can be changed"，由此我们可以换一种思路：当遇到要移除的项时，把它与数组最后一个元素交换位置并释放最后一个元素，这样可以减少赋值操作次数。具体如下：</h5>
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
      inputValue: JSON.stringify({
        nums: [1, 2, 2, 3, 3, 4],
        val: 3
      }),
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(nums,val) {
        const len = nums.length;
        let cur = -1;
        for(let i = 0;i<nums.length;i++){
            if(nums[i]!==val){
                nums[cur++]=nums[i];
            }
        }
        return cur+1;
    };`,
        "2": `
    submit(nums,val) {
        let i = 0;
        let n = nums.length;
        while(i<n){
            if(nums[i]==val){
                nums[i]=nums[n-1];
                n--;
            }else{
                i++;
            }
        }
        return n;
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
      const method = this[`method${this.activeTab}`],
        params = JSON.parse(this.inputValue),
        nums = params.nums,
        val = params.val;
      console.log("nums", nums, "val", val);
      method && method(nums, val);
    },
    /**
     * @param {array} nums
     * @param {number} val
     * @return {String}
     */
    method1(nums, val) {
      try {
        const len = nums.length;
        if (!len) {
          this.result = "[]";
          this.execute = "success";
          return;
        }
        let cur = 0;
        for (let i = 0; i < nums.length; i++) {
          if (nums[i] !== val) {
            nums[cur++] = nums[i];
          }
        }
        nums.length = cur;
        this.result = `[${nums.join(",")}]`;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    method2(nums, val) {
      try {
        let len = nums.length;
        if (!len) {
          this.result = "[]";
          this.execute = "success";
          return;
        }
        let cur = 0;
        while (cur < len) {
          if (nums[cur] == val) {
            nums[cur] = nums[len - 1];
            len--;
          } else {
            cur++;
          }
        }
        nums.length = cur;
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