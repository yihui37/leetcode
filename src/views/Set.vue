
 <template>
  <div class="setWrap">
    <h1>LeetCode习题集{{this.$route.params.id}}</h1>
    <el-collapse
      accordion
      v-model="activeName"
    >
      <el-collapse-item name="1">
        <template slot="title">Two Sum
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <TwoSum></TwoSum>
      </el-collapse-item>
      <el-collapse-item name="2">
        <template slot="title">Reverse Integer
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <ReverseInteger></ReverseInteger>
      </el-collapse-item>
      <el-collapse-item name="3">
        <template slot="title">Palindrome Number
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <PalindromeNumber></PalindromeNumber>
      </el-collapse-item>
      <el-collapse-item name="4">
        <template slot="title"> Roman to Integer
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <RomanToInteger></RomanToInteger>
      </el-collapse-item>
      <el-collapse-item name="5">
        <template slot="title"> Longest Common Prefix
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <LongestCommonPrefix></LongestCommonPrefix>
      </el-collapse-item>
      <el-collapse-item name="6">
        <template slot="title"> Valid Parentheses
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <ValidParentheses></ValidParentheses>
      </el-collapse-item>
      <el-collapse-item name="7">
        <template slot="title"> Merge Two Sorted Lists
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <MergeTwoSortedLists></MergeTwoSortedLists>
      </el-collapse-item>
      <el-collapse-item name="8">
        <template slot="title"> Remove Duplicates from Sorted Array
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <RemoveDuplicatesfromSortedArray></RemoveDuplicatesfromSortedArray>
      </el-collapse-item>
      <el-collapse-item name="9">
        <template slot="title"> Remove Element
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon"></i>
        </template>
        <RemoveElement></RemoveElement>
      </el-collapse-item>
      <el-collapse-item name="10">
        <template slot="title"> Count and Say
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <CountAndSay></CountAndSay>
      </el-collapse-item>
      <el-collapse-item name="11">
        <template slot="title"> Maximum Subarray
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <MaximumSubarray></MaximumSubarray>
      </el-collapse-item>
      <el-collapse-item name="12">
        <template slot="title"> Plus One
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <PlusOne></PlusOne>
      </el-collapse-item>
      <el-collapse-item name="13">
        <template slot="title"> Add Binary
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <AddBinary></AddBinary>
      </el-collapse-item>
      <el-collapse-item name="14">
        <template slot="title"> Sqrt(X)
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <SqrtX></SqrtX>
      </el-collapse-item>
      <el-collapse-item name="15">
        <template slot="title"> Climbing Stairs
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <ClimbingStairs></ClimbingStairs>
      </el-collapse-item>
      <el-collapse-item name="16">
        <template slot="title"> Symmetric Tree
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <SymmetricTree></SymmetricTree>
      </el-collapse-item>
      <el-collapse-item name="17">
        <template slot="title"> Binary Tree Level Order Traversal II
          <el-tag type="success">EASY</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <BinaryTreeLevelOrderTraversalII></BinaryTreeLevelOrderTraversalII>
      </el-collapse-item>
      <el-collapse-item name="18">
        <template slot="title"> Convert Sorted List to Binary Search Tree
          <el-tag type="warning">MEDIUM</el-tag>
          <i class="header-icon el-icon-star-on"></i>
        </template>
        <ConvertSortedListToBinarySearchTree></ConvertSortedListToBinarySearchTree>
      </el-collapse-item>
    </el-collapse>
    <el-button
      v-if="activeName"
      class="toggleBtn el-icon-arrow-up"
      type="warning"
      size="small"
      @click="activeName=''"
    >&nbsp;收起</el-button>
  </div>
</template>
 
 <script>
import TwoSum from "../components/set/TwoSum.vue";
import ReverseInteger from "../components/set/ReverseInteger.vue";
import PalindromeNumber from "../components/set/PalindromeNumber.vue";
import RomanToInteger from "../components/set/RomanToInteger.vue";
import LongestCommonPrefix from "../components/set/LongestCommonPrefix.vue";
import ValidParentheses from "../components/set/ValidParentheses.vue";
import MergeTwoSortedLists from "../components/set/MergeTwoSortedLists.vue";
import RemoveDuplicatesfromSortedArray from "../components/set/RemoveDuplicatesfromSortedArray.vue";
import RemoveElement from "../components/set/RemoveElement.vue";
import CountAndSay from "../components/set/CountAndSay.vue";
import MaximumSubarray from "../components/set/MaximumSubarray.vue";
import PlusOne from "../components/set/PlusOne.vue";
import AddBinary from "../components/set/AddBinary.vue";
import SqrtX from "../components/set/SqrtX.vue";
import ClimbingStairs from "../components/set/ClimbingStairs.vue";
import SymmetricTree from "../components/set/SymmetricTree.vue";
import BinaryTreeLevelOrderTraversalII from "../components/set/BinaryTreeLevelOrderTraversal-II";
import ConvertSortedListToBinarySearchTree from "../components/set/ConvertSortedListToBinarySearchTree";

export default {
  components: {
    TwoSum,
    ReverseInteger,
    PalindromeNumber,
    RomanToInteger,
    LongestCommonPrefix,
    ValidParentheses,
    MergeTwoSortedLists,
    RemoveDuplicatesfromSortedArray,
    RemoveElement,
    CountAndSay,
    MaximumSubarray,
    PlusOne,
    AddBinary,
    SqrtX,
    ClimbingStairs,
    SymmetricTree,
    BinaryTreeLevelOrderTraversalII,
    ConvertSortedListToBinarySearchTree
  },
  watch: {
    "$route.params": {
      handler(newValue) {
        if (newValue.id) {
          this.activeName = String(newValue.id);
          return;
        } else {
          this.$router.push({ path: "/set/1" });
        }
      },
      immediate: true,
      deep: true
    }
  },
  data() {
    return {
      activeName: "1"
    };
  },
  methods: {
    name() {}
  }
};
</script>
 
 <style lang="scss">
.el-tag {
  margin-left: 10px;
}
.header-icon {
  margin-left: 15px;
}
.el-collapse-item__wrap {
  background-color: #d1e4f7;
  padding: 10px;
}
.toggleBtn {
  position: fixed;
  right: 10px;
  bottom: 20px;
}
.exerciseItemWrap {
  text-align: left;
  .mainTitle {
    text-align: center;
    a {
      color: #409eff;
    }
  }
  pre {
    padding: 10px;
    min-height: 30px;
    background-color: #ecf5ff;
    border-left: 3px solid #333;
    &.success {
      border-color: #67c23a;
    }
    &.error {
      border-color: #f56c6c;
    }
  }
}
</style>