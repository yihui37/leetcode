<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Binary Tree Level Order Traversal II</a></h3>
      <section>
        <h4 class="subTitle">No.107 Question:</h4>
        <p>Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).</p>
        <p>For example:</p>
        <p>
          <pre>Given binary tree [3,9,20,null,null,15,7],</pre>
          <img
            src="https://ws2.sinaimg.cn/large/006tKfTcgy1g0f75hzgjfj306y06o0so.jpg"
            alt=""
          >
        </p>
        <p>
          <pre>return its bottom-up level order traversal as:</pre>
          <img
            src="https://ws4.sinaimg.cn/large/006tKfTcgy1g0f76dccpuj305u06mmx4.jpg"
            alt=""
          >
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
        <h5>我的第一次解法 将TreeNode的每层node暂存到一个堆栈中，遍历堆栈中的每个node，将值添加到层结果数组中，将node的左右非null子节点存储到层node数组中，将层结果数组存放到最终结果的开头，将层node数组替换堆栈，进行下一次堆栈遍历。具体如下：</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputValue: "[3,9,20,null,null,15,7]",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(root) {
        if(root==null) return [];
        let stack = [root],
            res = [];
        while(stack.length>0){
            let tmp = [],
                res_each = [];
            for(let node of stack){
                res_each.push(node.val);
                node.left !== null && tmp.push(node.left);
                node.right !== null && tmp.push(node.right);
            }
            stack = tmp;
            res.unshift(res_each);
        }
        return res;
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
      const params = {
        val: 3,
        left: {
          val: 9,
          left: null,
          right: null
        },
        right: {
          val: 20,
          left: {
            val: 15,
            left: null,
            right: null
          },
          right: {
            val: 7,
            left: null,
            right: null
          }
        }
      };
      method && method(params);
    },
    /**
     * @param {TreeNode} root
     * @return {number[][]}
     */
    // 每层遍历
    method1(root) {
      try {
        let stack = [root],
          res = [];
        while (stack.length > 0) {
          let tmp = [],
            res_each = [];
          for (let node of stack) {
            res_each.push(node.val);
            node.left !== null && tmp.push(node.left);
            node.right !== null && tmp.push(node.right);
          }
          stack = tmp;
          res.unshift(res_each);
        }
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