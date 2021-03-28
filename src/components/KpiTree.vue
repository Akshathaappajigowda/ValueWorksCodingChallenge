<template>
  <div>
    <h1>{{ msg }}</h1>
    <KpiSubTree :treeNode="[tree]"/>
  </div>
</template>

<script>
import  KpiSubTree  from "./KpiSubTree";

export default {
  name: 'KpiTree',
  props: {
    msg: String
  },
  components: {
    KpiSubTree
  },
  data: function() {
      return {
          tree: {
            name: "EDITDA", 
            value: {amount: "123", color: "green"}, 
            delta: {amount:"12%", color: "green"}, 
            children: [
              {
                name: "Customer Profitability",
                value: {amount: "123", color: "green"}, 
                delta: {amount: "12%", color: "red"}, 
                children: [
                  {
                    name: "MRR", 
                    value: {amount: "123", color: "orange"}, 
                    delta: {amount: "12%", color: "green"}, 
                    children: [
                      {
                        name: "ACV",
                        value: {amount: "123", color: "orange"}, 
                        delta: {amount: "12%", color: "red"}, 
                      }
                    ]
                  },
                  {
                    name: "Total CAC",
                    value: {amount: "123", color: "green"}, 
                    delta: {amount: "12%", color: "green"}, 
                    children: [
                      {
                        name: "Customer Success",
                        value: {amount: "123", color: "red"}, 
                        delta: {amount: "12%", color: "green"},
                      },
                      {
                        name: "Sales & Marketing",
                        value: {amount: "123", color: "green"}, 
                        delta: {amount: "12%", color: "green"},
                      }
                    ],
                  }
                ]
              },
              {
                name: "NON-CAC related",
                value: {amount: "123", color: "green"}, 
                delta: {amount:"12%", color: "orange"},
                children: [
                  {
                    name: "R&D (excl. Support)",
                    value: {amount: "123", color: "green"}, 
                    delta: {amount: "12%", color: "green"},                      
                  },
                  {
                    name: "G&A",
                    value: {amount: "123", color: "green"}, 
                    delta: {amount: "12%", color: "green"},  
                  }
                ]                 
              }
            ]
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.childLevel::before{  
  content: "";
  position: absolute;
  left: 50%;
  bottom: 100%;
  height: 15px;
  border-left: 2px solid red;
  transform: translate3d(-1px, 0, 0);

}
.childLevel::after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  top: -15px;
  border-top: 2px solid red;
}
.childLevel:first-child:before,
.childLevel:last-child:before {
  display: none;
}
.childLevel:first-child:after {
  left: 50%;
  height: 15px;
  border: 2px solid;
  border-color: rgb(104, 28, 28) transparent transparent rgb(58, 16, 16);
  border-radius: 6px 0 0 0;
  transform: translate3d(1px, 0, 0);
}
.childLevel:last-child:after {
  right: 50%;
  height: 15px;
  border: 2px solid;
  border-color: red red transparent transparent;
  border-radius: 0 6px 0 0;
  transform: translate3d(-1px, 0, 0);
}
.childLevel:first-child.childLevel:last-child::after {
  left: auto;
  border-radius: 0;
  border-color: transparent rgb(155, 58, 58) transparent transparent;
  transform: translate3d(1px, 0, 0);
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
