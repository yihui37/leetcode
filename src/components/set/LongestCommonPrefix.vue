<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle">Longest Common Prefix</h3>
      <section>
        <h4 class="subTitle">No.14 Question:</h4>
        <p>Write a function to find the longest common prefix string amongst an array of strings.<br>If there is no common prefix, return an empty string "".</p>
        <p>
          <b>Example 1:</b>
          <pre><b>Input:</b> ["flower","flow","flight"]<br><b>Output:</b> "fl"</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre><b>Input:</b> ["dog","racecar","car"]<br><b>Output:</b> ""<br><b>Explanation:</b> There is no common prefix among the input strings.</pre>
        </p>
        <p><b>Note:</b></p>
        <p>All given inputs are in lowercase letters a-z.</p>
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
        label="解法一  32.71% 76ms"
        name="1"
      >
        <h5>我的第一次解法 取数组中最后一个元素来遍历每一个字符，用正则校验剩余数组中每一个元素是否以此开头，是则保存这个字符并继续，否则退出当前存储字符串</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  44.32% 72ms"
        name="2"
      >
        <h5>使用.startsWith(String prefix, int toffset)方法代替正则匹配，使用第一个元素作为校验值，不匹配则依次去掉元素的最后一个字符继续匹配，直到匹配到全部符合的prefix</h5>
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
      inputValue: "abc,abcde,abmn",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(strs) {
        if(!strs.length) return "";
        let last = strs.pop().split(""),
            prefix = "";
        for (let i = 0; i < last.length; i++) {
            let reg = new RegExp('^'+ prefix + last[i]);
            let flag = strs.find(item => !reg.test(item));
            if (flag !== undefined) return prefix;
            prefix += last[i];
        }
        return prefix;
    };`,
        "2": `
    submit(strs) {
        if (strs.length == 0) return "";
        let prefix = strs[0];
        for(let i=0 ; i < strs.length; i++){
            while(! strs[i].startsWith(prefix) ){
                prefix = prefix.substring(0, prefix.length-1);
            }
        }
        return prefix
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
    submit() {
      const method = this[`method${this.activeTab}`];
      method && method(this.inputValue.split(","));
    },
    /**
     * @param {array} strs
     * @return {String}
     */
    //正则 从0到all匹配
    method1(strs) {
      try {
        if (strs.length == 0) {
          this.result = "''";
          this.execute = "success";
          return;
        }
        strs = strs.map(str => str.toLowerCase());
        const last = strs.pop().split("");
        let prefix = "";
        for (let i = 0; i < last.length; i++) {
          const reg = new RegExp(`^${prefix}${last[i]}`);
          const flag = strs.find(item => !reg.test(item));
          if (flag !== undefined) {
            this.result = prefix || "''";
            this.execute = "success";
            return;
          }
          prefix += last[i];
        }
        this.result = prefix;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // startsWith  从all到0匹配
    method2(strs) {
      try {
        if (strs.length == 0) return "";
        let prefix = strs[0];
        for (let i = 0; i < strs.length; i++) {
          while (!strs[i].startsWith(prefix)) {
            prefix = prefix.substring(0, prefix.length - 1);
          }
        }
        this.result = prefix || "''";
        this.execute = "success";
        return;
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