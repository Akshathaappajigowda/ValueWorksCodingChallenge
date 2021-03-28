<template >
  <table>
    <div class="element">    
      <table>
        <tr>
          <td>{{name}}</td> 
          <td class="expand-icon-before" v-if="Array.isArray(children) && expanded"  v-on:click="toggle"></td>
          <td class="expand-icon-after" v-else-if="Array.isArray(children)" v-on:click="toggle"></td>
        </tr>
        <tr>
          <td :style="{color:value.color}">{{ value.amount }}</td>
          <td :class="[delta.color]">▲</td>
          <td>{{ delta.amount }}</td>
        </tr> 
      </table> 
    </div>
    <div>
      <KpiSubTree v-if="expanded" :treeNode="children"/>
    </div>
  </table>
</template>

<script>
import KpiSubTree from "./KpiSubTree";

export default {
  name: "KpiTreeNode",
  props: {
    name: String,
    value: { amount: String, color: String },
    delta: { amount: String, color: String },
    children: Array
  },
  components: {
    KpiSubTree
  },
  data: function() {
    return {
      expanded: false
    }
  },
  methods:{
    toggle: function(){
      this.expanded = !this.expanded;
    }
  }
};
</script>

<style scoped>

.element {
  padding-top: 0;
  border-spacing: 10px ;
  align-items: center;
  background-color: gray;
  color: white;
  justify-content: center;
  display: inline-flex;
}

table{
  text-align: center;
  margin: 5px 5px 5px 5px;
  justify-content: center;
  display: inline-block;
}

.green{
  color: green;
}
.orange{
  color: orangered;
  transform:rotate(90deg);
  
}
.red{
  color: red;
  transform:rotate(180deg);
}
.expand-icon-after{
  background-image: url("../assets/image/up-arrow.svg");
  height: 20px;
  width: 20px;
  align-items: center;
}
.expand-icon-before{
  background-image: url("../assets/image/right-arrow.svg");
  height: 20px;
  width: 20px;
  align-items: center;
}
</style>