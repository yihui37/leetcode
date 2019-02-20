<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a
          href="https://leetcode-cn.com/articles/symmetric-tree/"
          target="_blank"
        >Symmetric Tree</a></h3>
      <section>
        <h4 class="subTitle">No.101 Question:</h4>
        <p>Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).</p>
        <p>For example, this binary tree [1,2,2,3,4,4,3] is symmetric:</p>
        <p>
          <img
            src="https://ws2.sinaimg.cn/large/006tKfTcgy1g0cpqhmubqj305q06k0so.jpg"
            alt=""
          >
        </p>
        <p>But the following [1,2,2,null,3,null,3] is not:</p>
        <p>
          <img
            src="https://ws2.sinaimg.cn/large/006tKfTcgy1g0cpr0mbrtj306k06uglj.jpg"
            alt=""
          >
        </p>
        <p>
          <b>Note:</b>Bonus points if you could solve it both recursively and iteratively.
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
        label="解法一  80ms"
        name="1"
      >
        <h5>我的第一次解法</h5>
        <p>在100题的经验下，将root二叉树copy一份作为镜像，对两个二叉树的镜面位置Node进行比较，具体如下：</p>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  84ms"
        name="2"
      >
        <h5>题干中说，如果可以用递归和迭代两种方法来解题会是个加分项，因此思考了一下迭代的方式。在之前LinkedList类型题目的提示下想到：仍然将root二叉树copy一份作为镜像，然后新建一个数组，依次将两个二叉树中的镜像位置的Node存放至数组中，则数组中的连续两个元素（镜像对应Node）值应当相等，由此进行判断。具体如下：</h5>
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
      inputValue: "[1,2,2,3,4,4,3]",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(root) {
        let judge = (left, right) => {
            if (left == null && right == null) return true;
            if (left == null || right == null) return false;
            return (
            left.val == right.val &&
            judge(left.left, right.right) &&
            judge(left.right, right.left)
            );
        };
        return judge(root, root);
    };`,
        "2": `
    submit(root) {
        let queue = new Array();
        queue.push(root);
        queue.push(root);
        while(queue.length){
            let t1 = queue.shift(),
                t2 = queue.shift();
            if(t1 == null && t2 == null) continue;
            if(t1 == null || t2 == null) return false;
            if(t1.val !== t2.val) return false;
            queue.push(t1.left);
            queue.push(t2.right);
            queue.push(t1.right);
            queue.push(t2.left);
        }
        return true;
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
          val: 2,
          left: {
            val: 4,
            left: null,
            right: null
          },
          right: {
            val: 3,
            left: null,
            right: null
          }
        }
      };
      method && method(params);
    },
    /**
     * @param {TreeNode} root
     * @return {boolean}
     */
    // 递归
    method1(root) {
      let judge = (left, right) => {
        if (left == null && right == null) return true;
        if (left == null || right == null) return false;
        return (
          left.val == right.val &&
          judge(left.left, right.right) &&
          judge(left.right, right.left)
        );
      };
      try {
        this.result = judge(root, root);
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 迭代
    method2(root) {
      try {
        let queue = new Array();
        queue.push(root);
        queue.push(root);
        while (queue.length) {
          let t1 = queue.shift(),
            t2 = queue.shift();
          if (t1 == null && t2 == null) continue;
          if (t1 == null || t2 == null) {
            this.result = false;
            this.execute = "success";
            return;
          }
          if (t1.val !== t2.val) {
            this.result = false;
            this.execute = "success";
            return;
          }
          queue.push(t1.left);
          queue.push(t2.right);
          queue.push(t1.right);
          queue.push(t2.left);
        }
        this.result = true;
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