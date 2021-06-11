<template>
  <div>
    <h3>基本初等函数</h3>
    <el-collapse v-model="activeName" accordion>
      <el-collapse-item
        v-for="(col, index) in collapse"
        :key="col.id"
        :title="col.title"
        :name="col.id"
      >
        <div>
          {{ col.content }}
        </div>
        <el-button type="primary" size="mini" @click="sumit(index)">查看详情</el-button>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeName: "1",
      collapse: [
        {
          id: 1,
          title: "幂函数",
          content: ` 一般地，形如y=xα(α为有理数）的函数，即以底数为自变量，幂为因变量，指数为常数的函数称为幂函数。例如函数y=x0
        、y=x1、y=x2、y=x-1（注：y=x-1=1/x y=x0时x≠0）等都是幂函数。一般形式如下
        [1] ： （ α为常数，且可以是自然数、有理数，也可以是任意实数或复数。）`,
        },
        {
          id: 2,
          title: "指数函数",
          content: ` 指数函数是数学中重要的函数。应用到值e上的这个函数写为exp(x)。还可以等价的写为ex，这里的e是数学常数，就是自然对数的底数，近似等于 2.718281828，还称为欧拉数。一般形式如下 [1]  ：
 （a>0, a≠1）`,
        },
        {
          id: 3,
          title: "对数函数",
          content: `一般地，函数y=logax（a>0，且a≠1）叫做对数函数，也就是说以幂（真数）为自变量，指数为因变量，底数为常量的函数，叫对数函数。
其中x是自变量，函数的定义域是（0，+∞），即x>0。它实际上就是指数函数的反函数，可表示为x=ay。因此指数函 数里对于a的规定，同样适用于对数函数。一般形式如下 [1]  ：
 （a>0, a≠1， x>0,特别当α=e时，记为y=ln x）`,
        },
      ],
    };
  },
  methods: {
    sumit(index) {
      let target = null;
      if (index == 0) {
        target = "Math.pow(x,3)";
      } else if (index == 1) {
        target = "Math.pow(2,x)";
      } else if (index == 2) {
        target = "Math.log(x)";
      }
      this.$emit("colData", target);
    },
  },
};
</script>