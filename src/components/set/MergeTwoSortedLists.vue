<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle"><a target="_blank">Merge Two Sorted Lists</a></h3>
      <section>
        <h4 class="subTitle">No.21 Question:</h4>
        <p>Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.</p>
        <p>
          <b>Example 1:</b>
          <pre><b>Input:</b> 1->2->4, 1->3->4<br><b>Output:</b> 1->1->2->3->4->4</pre>
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
        label="解法一  88ms"
        name="1"
      >
        <h5>我的第一次解法 磕磕绊绊bug了好多次。</h5>
        <ul>
          <li><b>1.如果l1或l2为空，则直接返回其一</b>这一点一开始没想到，一直在纠结如何针对空对象做容错处理，没有第一时间反应过来如果其一为空则结果为另一参数</li>
          <li>2.整体思路为，将l2中Node拆解出来一个一个和l1中的Node的val比较大小插入到正确的位置</li>
          <li>3.容易忽略的点
            <ul>
              <li>不要理想化的认为l1就是多节点</li>
              <li>不要忘了l2的Node比l1第一个节点小的情况（插入最前面）</li>
            </ul>
          </li>
        </ul>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  84ms"
        name="2"
      >
        <h5>通过新链表来存储两个链表每次比较的较小Node，具体看代码注释</h5>
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
        l1: {
          val: 2
        },
        l2: {
          val: 1
        }
      }),
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(l1, l2) {
        if(!l1 || !l2) return l1||l2;
        while (l2) {
            let node = {
                val: l2.val,
                next: undefined
            };
            l2 = l2.next;
            insertNode(l1, node);
        }
        return l1;
    };

    var insertNode = (list,node)=>{
        let nextNodeList = list.next;
        if (node.val < list.val) {
            // 比当前node小，往前排
            const curNode = Object.assign({}, list);
            list = Object.assign(list, {
                val: node.val,
                next: curNode
            });
        } else if (nextNodeList == undefined) {
            // 最后一个，直接追加
            list.next = Object.assign(node, {
                next: nextNodeList
            });
        } else if (node.val >= list.val && node.val < list.next.val) {
            list.next = Object.assign(node, {
                next: nextNodeList
            });
        } else {
            insertNode(nextNodeList, node);
        }
    }`,
        "2": `
    submit(strs) {
        let preNode = new ListNode(-1)  // 新建一个链表
        let cur = preNode               // 指针指向第一个
        while(l1 && l2){                // 两个链表都没有结束
            if(l1.val<l2.val){          // 比较两个链表第一个Node值
                cur.next = l1           // 较小的那个Node链到新链表里
                cur = cur.next          // 新链表的指针指向下一个
            
                l1 = l1.next            // 链出的链表指针指向下一个
            }else{
                cur.next = l2
                cur = cur.next
                l2 = l2.next 
            }
        }
        
        cur.next = l1 || l2             // 将剩余未链接完毕的nodeList直接链到最后
        return preNode.next             // 注意正确的存储从新链表的第二个Node开始
    }`
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
        l1 = params.l1,
        l2 = params.l2;
      method && method(l1, l2);
    },
    /**
     * @param {Object} l1
     * @param {Object} l2
     * @return {Object}
     */
    //将list2中的node一个一个插入到l1中
    method1(l1, l2) {
      try {
        if (!l1 || !l2) {
          this.result = l1 || l2;
          this.execute = "success";
          return;
        }
        while (l2) {
          let node = {
            val: l2.val
          };
          l2 = l2.next;
          this.insertNode(l1, node);
        }
        this.result = l1;
        this.execute = "success";
      } catch (err) {
        console.log(err);
        this.result = err;
        this.execute = "error";
      }
    },
    insertNode(list, node) {
      let nextNodeList = list.next;
      if (node.val < list.val) {
        // 比当前node小，往前排
        const curNode = Object.assign({}, list);
        list = Object.assign(list, {
          val: node.val,
          next: curNode
        });
      } else if (nextNodeList == undefined) {
        // 最后一个，直接追加
        list.next = Object.assign(node, {
          next: nextNodeList
        });
      } else if (node.val >= list.val && node.val < list.next.val) {
        list.next = Object.assign(node, {
          next: nextNodeList
        });
      } else {
        this.insertNode(nextNodeList, node);
      }
    },
    // startsWith  从all到0匹配
    method2(l1, l2) {
      try {
        let preNode = { val: -1, next: null }; // 新建一个链表
        let cur = preNode; // 指针指向第一个
        while (l1 && l2) {
          // 两个链表都没有结束
          if (l1.val < l2.val) {
            // 比较两个链表第一个Node值
            cur.next = l1; // 较小的那个Node链到新链表里
            cur = cur.next; // 新链表的指针指向下一个

            l1 = l1.next; // 链出的链表指针指向下一个
          } else {
            cur.next = l2;
            cur = cur.next;
            l2 = l2.next;
          }
        }
        cur.next = l1 || l2; // 将剩余未链接完毕的nodeList直接链到最后
        this.result = preNode.next;
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