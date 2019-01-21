<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a
          href="https://leetcode-cn.com/articles/valid-parentheses/"
          target="_blank"
        >Valid Parentheses</a></h3>
      <section>
        <h4 class="subTitle">No.20 Question:</h4>
        <p>Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.<br>An input string is valid if:
          <ul>
            <li>1.Open brackets must be closed by the same type of brackets.</li>
            <li>2.Open brackets must be closed in the correct order.</li>
          </ul>
          <br>Note that an empty string is also considered valid.
        </p>
        <p>
          <b>Example 1:</b>
          <pre><b>Input:</b> "()"<br><b>Output:</b> true</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre><b>Input:</b> "()[]{}"<br><b>Output:</b> true</pre>
        </p>
        <p>
          <b>Example 3:</b>
          <pre><b>Input:</b> "(]"<br><b>Output:</b> false</pre>
        </p>
        <p>
          <b>Example 4:</b>
          <pre><b>Input:</b> "([)]"<br><b>Output:</b> false</pre>
        </p>
        <p>
          <b>Example 5:</b>
          <pre><b>Input:</b> "{[]}"<br><b>Output:</b> true</pre>
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
        <h5>我的第一次解法 将括号匹配信息以对象的键值对形式存储，定义一个顺序空数组，遍历字符串，如果顺序数组中最后一个元素和当前元素是配对的，则抛出最后一个元素，否则向顺序数组中添加当前元素。</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  68ms"
        name="2"
      >
        <h5>上一解中判断如果为空字符串则直接返回true，想到如果字符串长度为奇数，也可直接返回false。</h5>
        <pre>
        <code>{{answers[2]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法三  68ms"
        name="3"
      >
        <h5>区分括号的开端和闭合，是开端符号的存储，是闭合符号的进行匹配判断，如果与顺序数组的最后一个不匹配可以直接返回false。</h5>
        <pre>
        <code>{{answers[3]}}</code>
      </pre>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: "[{}]",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(s) {
        len = s.length;
        if(len==0) return true;
        let match = {
            '(':')',
            '{':'}',
            '[':']'
        },
            order = [];
        for(let i=0;i<s.length;i++){
            if(match[order[order.length-1]]==s[i]){
                order.pop();
            }else{
                order.push(s[i]);
            }
        }
        return order.length == 0;
    };`,
        "2": `
    submit(s) {
        len = s.length;
        if(len==0) return true;
        if(len%2==1) return false;
        let match = {
            '(':')',
            '{':'}',
            '[':']'
        },
            order = [];
        for(let i=0;i<s.length;i++){
            if(match[order[order.length-1]]==s[i]){
                order.pop();
            }else{
                order.push(s[i]);
            }
        }
        return order.length == 0;
    };`,
        "3": `
    submit(s) {
        len = s.length;
        if(len==0) return true;
        if(len%2==1) return false;
        var match = {
            ')':'(',
            '}':'{',
            ']':'['
        },
            order = [];
        for(let i=0;i<s.length;i++){
            var matchItem = match[s[i]];
            if(matchItem){
                if(order[order.length-1]!==matchItem) return false;
                order.pop();
            }else{
                order.push(s[i]);
            }
        }
        return order.length == 0;
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
    submit() {
      const method = this[`method${this.activeTab}`];
      method && method(this.inputValue);
    },
    /**
     * @param {String} inputValue
     * @return {boolean}
     */
    //正则 从0到all匹配
    method1(s) {
      try {
        if (s.length == 0) {
          this.result = true;
          this.execute = "success";
          return;
        }
        let match = {
            "(": ")",
            "{": "}",
            "[": "]"
          },
          order = [];
        for (let i = 0; i < s.length; i++) {
          if (match[order[order.length - 1]] == s[i]) {
            order.pop();
          } else {
            order.push(s[i]);
          }
        }
        this.result = order.length == 0;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 多一个奇数长度判断
    method2(s) {
      try {
        if (s.length == 0) {
          this.result = true;
          this.execute = "success";
          return;
        }
        if (s.length % 2 !== 0) {
          this.result = false;
          this.execute = "success";
          return;
        }
        let match = {
            "(": ")",
            "{": "}",
            "[": "]"
          },
          order = [];
        for (let i = 0; i < s.length; i++) {
          if (match[order[order.length - 1]] == s[i]) {
            order.pop();
          } else {
            order.push(s[i]);
          }
        }
        this.result = order.length == 0;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 区分闭合括号，进行匹配判断
    method3(s) {
      try {
        s = s.trim();
        if (s.length == 0) {
          this.result = true;
          this.execute = "success";
          return;
        }
        if (s.length % 2 !== 0) {
          this.result = false;
          this.execute = "success";
          return;
        }
        const match = {
            ")": "(",
            "}": "{",
            "]": "["
          },
          order = [];
        for (let i = 0; i < s.length; i++) {
          var matchItem = match[s[i]];
          if (matchItem) {
            if (order[order.length - 1] == matchItem) {
              order.pop();
            } else {
              this.result = false;
              this.execute = "success";
              return;
            }
          } else {
            order.push(s[i]);
          }
        }
        this.result = order.length == 0;
        this.execute = "success";
        return;
      } catch (err) {
        console.log(err);
        this.result = err;
        this.execute = "error";
      }
    }
  }
};
</script>

<style scoped>
</style>