<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Triangle</a></h3>
      <section>
        <h4 class="subTitle">No.120 Question:</h4>
        <p>Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.</p>
        <p>
          <pre>For example, given the following triangle</pre>
          <img
            src="https://ws1.sinaimg.cn/large/006tKfTcgy1g0n543za14j307m082dfw.jpg"
            alt=""
          >
        </p>
        <p>The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).</p>
        <p>
          <b>Note:</b>
          Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.
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
        label="解法一  ❌"
        name="1"
      >
        <h5>我的第一次解法 <el-tag type="danger">整体想错：并不是取每一层的最小值相加，而是取所有路径的最小和。</el-tag>
        </h5>
        <p>从第一层第一个数0开始自顶向下找出相邻两个数中的较小值，计入总和。本来想的很简单，只要找到较小值并记录，继续下一层的相邻两个值比较直到结束就完成。</p>
        <p>但后来想到自己忽略了如果相邻值大小相等，则在下一层需要考虑大于2个的相邻值。于是想到存储每层中最小值（可多个），并记录它们各自的位置，在下一层循环遍历一个候选值的相邻节点，直到找到最底层。</p>
        <p>具体如下：</p>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  60ms"
        name="2"
      >
        <h5>尾部递归，将第n行和第n-1行合并, 且n-1行的值是合并后最小的值。</h5>
        <p>与第一种解法区别在于，它虽然也是逐行遍历取相邻两个元素的较小值，但它遍历了每一个元素，记录了所有可能性。</p>
        <p>三角形的合并顺序为: [6,5,7] + [4,1,8,3] = [6 + 1, 5 + 1, 7 + 3] = [7,6,10]; [3,4] + [7,6,10] = [3 + 6, 4 + 6] = [9, 10]; [2] + [9, 10] = [11];</p>
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
      inputValue: [[-1], [2, 3], [1, -1, -3]],
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(a,b) {
        const rows = triangle.length;
        if (rows==0) return 0;
        let indexArr = [0],    //  当同一层的可选项值相等时，下一层需考虑多个元素
            sum = 0;
        for(let row = 0;row<rows;row++){
            const valueArr = triangle[row];
            let min = valueArr[indexArr[0]];
            for(let i of indexArr){
                if(valueArr[i]<min){
                    min = valueArr[i];
                    indexArr = [i];
                }
                
                if(valueArr[i+1]<min){
                    min = valueArr[i+1];
                    indexArr = [i+1];
                }else if(valueArr[i+1]==min){
                    indexArr.push(i+1);
                }
            }
            sum +=min;
        }
        return sum;
    };`,
        "2": `
    submit(a,b) {
        let sum = triangle[triangle.length - 1];
        for (let i = triangle.length - 2; i >= 0; i--) {
          for (let j = 0; j < triangle[i].length; j++) {
            sum[j] = triangle[i][j] + Math.min(sum[j], sum[j + 1]);
          }
        }
        return sum[0];
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
     * @param {number[][]} triangle
     * @return {number}
     */
    // 考虑每层可能会有相同的最小值
    method1(triangle) {
      try {
        const rows = triangle.length;
        if (rows == 0) return 0;
        let indexArr = [0], //  记录同层中相同最小值的位置，下层遍历比较所有位置的相邻节点
          sum = 0;
        for (let row = 0; row < rows; row++) {
          debugger;
          const valueArr = triangle[row];
          let min = valueArr[indexArr[0]];
          for (let i of indexArr) {
            if (valueArr[i] < min) {
              // 更新替换最小值
              min = valueArr[i];
              indexArr = [i];
            }

            if (valueArr[i + 1] < min) {
              // 更新替换最小值
              min = valueArr[i + 1];
              indexArr = [i + 1];
            } else if (valueArr[i + 1] == min) {
              // 添加相同最小值的位置
              indexArr.push(i + 1);
            }
          }
          sum += min;
        }
        this.result = sum;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 尾部递归
    method2(triangle) {
      try {
        let sum = triangle[triangle.length - 1];
        for (let i = triangle.length - 2; i >= 0; i--) {
          for (let j = 0; j < triangle[i].length; j++) {
            sum[j] = triangle[i][j] + Math.min(sum[j], sum[j + 1]);
          }
        }
        this.result = sum[0];
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