<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Convert Sorted List to Binary Search Tree</a></h3>
      <section>
        <h4 class="subTitle">No.109 Question:</h4>
        <p>Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.</p>
        <p>For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.</p>
        <p><b>Example:</b></p>
        <p>
          <pre>Given the sorted linked list: [-10,-3,0,5,9],<br>One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:</pre>
          <img
            src="https://ws3.sinaimg.cn/large/006tKfTcgy1g0jrytzyp2j304q06et8n.jpg"
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
        label="解法一  ❓"
        name="1"
      >
        <h5>我的第一次解法 依次遍历链表中的node填充到二叉树中。具体如下：</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
        <p>提交后显示为错误答案:<br>
          <img
            src="https://ws4.sinaimg.cn/large/006tKfTcgy1g0juo8b0nqj30ia09mt9b.jpg"
            alt=""
            height="200"
          ><br>
          但是在题目 <a
            href="https://leetcode.com/problems/balanced-binary-tree/"
            target="_blank"
          >110. Balanced Binary Tree</a>中，将我的输出结果拿去验证，却是验证成功<br>
          <img
            src="https://ws3.sinaimg.cn/large/006tKfTcgy1g0jum0sdpkj30cy0a4t91.jpg"
            alt=""
            height="150"
          ><br>
          即是一个符合条件的高度平衡二叉树，不知哪里出了问题，无法通过，如有知道的，还请不吝赐教。
        </p>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  76ms "
        name="2"
      >
        <h5>为保证创建一个‘height-balanced’的二叉树，首先将链表转化为一个数组，然后取数组中间值作为根节点，再将数组从中间分为左右两个数组，作为根的左右子节点，再以同样方式建立各个叶子节点。具体如下：</h5>
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
      inputValue: "[-10,-3,0,5,9]",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(head) {
        if(head==null) return null;
        let root = new TreeNode(head.val);
        let curLevelTreeNode = [root];
        while(head!==null){
            let nodeTmp = [];
            for(let node of curLevelTreeNode){
                head = head.next;
                if(head==null) break;
                node.left = new TreeNode(head.val);
                nodeTmp.push(node.left);
                head = head.next;
                if(head==null) break;
                node.right = new TreeNode(head.val);
                nodeTmp.push(node.right);
            }
            curLevelTreeNode = nodeTmp;
        }
        return root;
    };`,
        "2": `
    submit(head) {
        if(head==null) return null;
        // 转为数组
        let arr = [];
        while(head!=null){
            arr.push(head.val);
            head = head.next;
        }
        
        // 将数组转化为二叉树
        return buildTree(arr,0,arr.length - 1);
    };
    var buildTree = function (nums,left,right){
        if(left > right) return null;
        if(left == right) return new TreeNode(nums[left]);
    
        let mid = parseInt((left + right) / 2),
            root = new TreeNode(nums[mid]);
        root.left = buildTree(nums,left,mid-1);
        root.right = buildTree(nums,mid + 1,right);
        return root;
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
        val: -10,
        next: {
          val: -3,
          next: {
            val: 0,
            next: {
              val: 5,
              next: {
                val: 9
              }
            }
          }
        }
      };
      method && method(params);
    },
    ListNode: function(val) {
      this.val = val;
      this.next = null;
    },
    TreeNode: function(val) {
      this.val = val;
      this.left = this.right = null;
    },
    /**
     * @param {ListNode} head
     * @return {TreeNode}
     */
    // 将head中node依次赋值填充二叉树
    method1(head) {
      try {
        if (head == null) return null;
        let root = new this.TreeNode(head.val);
        let curLevelTreeNode = [root];
        while (head != null) {
          let nodeTmp = [];
          for (let node of curLevelTreeNode) {
            head = head.next;
            if (head == null) break;
            node.left = new this.TreeNode(head.val);
            nodeTmp.push(node.left);
            head = head.next;
            if (head == null) break;
            node.right = new this.TreeNode(head.val);
            nodeTmp.push(node.right);
          }
          curLevelTreeNode = nodeTmp;
        }
        this.result = root;
        this.execute = "success";
      } catch (err) {
        console.log(err);
        this.result = err;
        this.execute = "error";
      }
    },
    // 从中间开始建立根节点
    method2(head) {
      try {
        if (head == null) return null;
        // 转为数组
        let arr = [];
        while (head != null) {
          arr.push(head.val);
          head = head.next;
        }
        // 将数组转化为二叉树
        this.result = this.buildTree(arr, 0, arr.length - 1);
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    buildTree(nums, left, right) {
      if (left > right) return null;
      if (left == right) return new this.TreeNode(nums[left]);

      let mid = parseInt((left + right) / 2),
        root = new this.TreeNode(nums[mid]);
      root.left = this.buildTree(nums, left, mid - 1);
      root.right = this.buildTree(nums, mid + 1, right);
      return root;
    }
  }
};
</script>

<style scoped>
</style>