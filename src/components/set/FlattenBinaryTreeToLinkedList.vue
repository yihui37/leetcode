<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Flatten Binary Tree to Linked List</a></h3>
      <section>
        <h4 class="subTitle">No.114 Question:</h4>
        <p>Given a binary tree, flatten it to a linked list in-place.</p>
        <p>For example, given the following tree:</p>
        <p>
          <img
            src="https://ws2.sinaimg.cn/large/006tKfTcgy1g0m6boho60j306a06m748.jpg"
            alt=""
          >
        </p>
        <p>
          <pre>The flattened tree should look like:</pre>
          <img
            src="https://ws1.sinaimg.cn/large/006tKfTcgy1g0m6c3cxqfj30aa0d6aa2.jpg"
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
        label="解法一  72ms"
        name="1"
      >
        <h5>我的第一次解法 题干中说改编成链表，误以为是以next的形式链接成链表，后来仔细看了一下是要求全部链接到右子树上。由此想到遍历每一个左子树，将左子树接到同层的右节点上，再将原来的右子树接到左子树的最后一个右节点上，依次处理每一个左子树。具体如下：</h5>
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
      inputValue: "[1,2,5,3,4,null,6]",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(root) {
        if (!root) return;
        this.method1(root.left);
        this.method1(root.right);
        if (root.left != null) {
          let tmp = root.right;
          root.right = root.left;
          // 不要忘了把左子树置空
          root.left = null;
          // 寻找左子树中的最后一个右节点
          let node = root.right;
          while (node.right != null) {
            node = node.right;
          }
          node.right = tmp;
        }
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
        val: 1,
        left: {
          val: 2,
          left: {
            val: 3,
            left: null,
            right: null
          },
          right: {
            val: 4,
            left: null,
            right: null
          }
        },
        right: {
          val: 5,
          left: null,
          right: {
            val: 6,
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
    // 将左子树转接到右子树
    method1(root) {
      try {
        if (!root) return;
        this.method1(root.left);
        this.method1(root.right);
        if (root.left != null) {
          let tmp = root.right;
          root.right = root.left;
          root.left = null;
          let node = root.right;
          // 寻找左子树中的最后一个右节点
          while (node.right != null) {
            node = node.right;
          }
          node.right = tmp;
        }
        this.result = root;
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