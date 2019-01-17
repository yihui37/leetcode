<template>
  <div class="exerciseItemWrap">
    <article>
      <h3 class="mainTitle">Roman to Integer</h3>
      <section>
        <h4 class="subTitle">No.13 Question:</h4>
        <p>Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.</p>
        <img
          src="https://ws3.sinaimg.cn/large/006tNc79gy1fz9dz5k70bj30as0a6t8x.jpg"
          alt=""
        >
        <p>For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

          Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

          I can be placed before V (5) and X (10) to make 4 and 9.
          X can be placed before L (50) and C (100) to make 40 and 90.
          C can be placed before D (500) and M (1000) to make 400 and 900.
          Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.
        </p>
        <p>
          <b>Example 1:</b>
          <pre><b>Input:</b> "III"<br><b>Output:</b> 3</pre>
        </p>
        <p>
          <b>Example 2:</b>
          <pre><b>Input:</b> "IV"<br><b>Output:</b> 4</pre>
        </p>
        <p>
          <b>Example 3:</b>
          <pre><b>Input:</b> "IX"<br><b>Output:</b> 9</pre>
        </p>
        <p>
          <b>Example 4:</b>
          <pre><b>Input:</b> "LVIII"<br><b>Output:</b> 58<br><b>Explanation:</b> L = 50, V= 5, III = 3.</pre>
        </p>
        <p>
          <b>Example 5:</b>
          <pre><b>Input:</b> "MCMXCIV"<br><b>Output:</b> 1994<br><b>Explanation:</b> M = 1000, CM = 900, XC = 90 and IV = 4.</pre>
        </p>
      </section>
    </article>
    <div class="paramsWrap">
      <h4 class="subTitle">Params</h4>
      <label>Input:</label>
      <el-input
        type="text"
        v-model="inputValue"
      ></el-input>
      <p>
        <el-button
          type="primary"
          @click="submit(inputValue)"
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
        label="解法一  28.67% 196ms"
        name="1"
      >
        <h5>我的第一次解法 将特殊的三个字母和六种组合情况存储起来，循环遍历输入的罗马数字字符，遇到特殊的三个字母则继续判断与下一个字符是否为六种组合，不是则直接相加，是则加组合对应值</h5>
        <pre>
        <code>{{answers[1]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法二  57.58% 188ms"
        name="2"
      >
        <h5>思路为：六种组合可以总结为使用第二个字符对应值减去第一个字符对应值即为该组合字符对应值，但对特殊字符的判断方法同第一种差不多</h5>
        <pre>
        <code>{{answers[2]}}</code>
      </pre>
      </el-tab-pane>
      <el-tab-pane
        label="解法三  32.95% 196ms"
        name="3"
      >
        <h5>思路为：使用<b>chartAt()</b>方法来取遍历中的字符串的值，当后一个字符比当前字符值大时则表明当前字符作减法，否则做加法</h5>
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
      inputValue: "MCMXCIV",
      result: "",
      execute: "",
      activeTab: "1",
      answers: {
        "1": `
    submit(x) {
        let roman = {
            "I":1,
            "V":5,
            "X":10,
            "L":50,
            "C":100,
            "D":500,
            "M":1000
        },
        specialArr = ["I","X","C"],
        special = {
            "IV":4,
            "IX":9,
            "XL":40,
            "XC":90,
            "CD":400,
            "CM":900
        };
        let arr = s.split(''),
            num = 0,
            jump = false;
        for(let [index,item] of arr.entries()){
            if (jump) {
                jump = false;
                continue;
            }
            let val = roman[item];
            if(val==undefined){
                return "啊哦，不是罗马数字";
            } else if(specialArr.includes(item)&& (index<arr.length -1)&&                       special[item + arr[index+1]]!==undefined){
                num += special[item + arr[index+1]];
                jump = true;
            }else{
                num += val;
                jump = false;
            }
        }
        if(num <1 || num >3999) return "啊哦，输入值超出限制范围";
        return num;
    };`,
        "2": `
    submit(x) {
        let xReverse = 0, xOrg = x;
        if (xOrg < 0) {
            return false;
        }
        while (x) {
            xReverse = xReverse * 10 + x % 10; 
            x = Math.floor(x/10);
        }
        if (xReverse === xOrg) {
            return true;
        }
        return false;
    }`,
        "3": `
    submit(x) {
        var map = {
            'I': 1,
            'V': 5,
            'X': 10,
            'L': 50,
            'C': 100,
            'D': 500,
            'M': 1000
        };
        let year = 0;
        
        for (let i=0; i<s.length; i++) {
            if(map[s.charAt(i+1)] > map[s.charAt(i)]) {
                year -= map[s.charAt(i)]
            } else {
                year += map[s.charAt(i)]
            }
        }
        return year;
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
     * @param {String} s
     * @return {Number}
     */
    submit(s) {
      const method = this[`method${this.activeTab}`];
      method && method(s);
    },
    method1(s) {
      try {
        let roman = {
            I: 1,
            V: 5,
            X: 10,
            L: 50,
            C: 100,
            D: 500,
            M: 1000
          },
          specialArr = ["I", "X", "C"],
          special = {
            IV: 4,
            IX: 9,
            XL: 40,
            XC: 90,
            CD: 400,
            CM: 900
          };
        let arr = s.split(""),
          num = 0,
          jump = false;
        for (let [index, item] of arr.entries()) {
          if (jump) {
            jump = false;
            continue;
          }
          let val = roman[item];
          if (val == undefined) {
            this.result = "啊哦，不是罗马数字";
            this.execute = "success";
            return;
          } else if (
            specialArr.includes(item) &&
            index < arr.length - 1 &&
            special[item + arr[index + 1]] !== undefined
          ) {
            num += special[item + arr[index + 1]];
            jump = true;
          } else {
            num += val;
            jump = false;
          }
        }
        if (num < 1 || num > 3999) {
          this.result = "啊哦，输入值超出限制范围";
          this.execute = "success";
        } else {
          this.result = num;
          this.execute = "success";
        }
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // 第二字符减第一字符值
    method2(s) {
      try {
        const value = {
          I: 1,
          V: 5,
          X: 10,
          L: 50,
          C: 100,
          D: 500,
          M: 1000
        };
        const order = ["I", "V", "X", "L", "C", "D", "M"];
        const indexOfDeductable = order.reduce((m, char, i) => {
          m[char] = ["I", "X", "C"].includes(char) ? i : undefined;
          return m;
        }, {});
        let sum = 0;
        for (let i = 0; i < s.length; i++) {
          const index = indexOfDeductable[s[i]];
          let num = value[s[i]];

          if (index !== undefined && i < s.length - 1) {
            const nextChar = s[i + 1];
            if (
              order[index + 1] === nextChar ||
              order[index + 2] === nextChar
            ) {
              num = value[nextChar] - num;
              i++; // skip next char
            }
          }

          sum += num;
        }
        this.result = sum;
        this.execute = "success";
      } catch (err) {
        this.result = err;
        this.execute = "error";
      }
    },
    // chartAt()方法取值
    method3(s) {
      try {
        const map = {
          I: 1,
          V: 5,
          X: 10,
          L: 50,
          C: 100,
          D: 500,
          M: 1000
        };
        let num = 0;

        for (let i = 0; i < s.length; i++) {
          if (map[s.charAt(i + 1)] > map[s.charAt(i)]) {
            num -= map[s.charAt(i)];
          } else {
            num += map[s.charAt(i)];
          }
        }
        this.result = num;
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