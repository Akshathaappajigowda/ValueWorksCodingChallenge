<template>
        <ul>
            <li v-for="node in treeNode" :key="node.name">
                <KpiTreeNode 
                    :name="node.name"
                    :value="node.value"
                    :delta="node.delta"
                    :children="node.children"/>
            </li>
        </ul>
</template>

<script>

export default {
    name: 'KpiSubTree',
    props: {
        treeNode: Array
    },
    components: {
        KpiTreeNode: () => import('./KpiTreeNode.vue')
    }
}
</script>

<style scoped>
ul {
	padding-top: 20px; position: relative;
	
	transition: all 0.5s;
	-webkit-transition: all 0.5s;
	-moz-transition: all 0.5s;
}

li {
	float: left; text-align: center; align-items: center;
	list-style-type: none;
	position: relative;
	padding: 20px 5px 0 5px;
	
	transition: all 0.5s;
	-webkit-transition: all 0.5s;
	-moz-transition: all 0.5s;
}

/*We will use ::before and ::after to draw the connectors*/

li::before, li::after{
	content: '';
	position: absolute; top: 0; right: 50%;
	border-top: 1px solid rgb(7, 5, 5);
	width: 50%; height: 20px;
}
li::after{
	right: auto; left: 50%;
	border-left: 1px solid rgb(7, 5, 5);
}

/*We need to remove left-right connectors from elements without 
any siblings*/
li:only-child::after, li:only-child::before {
	display: none;
}

/*Remove space from the top of single children*/
li:only-child{ padding-top: 0;}

/*Remove left connector from first child and 
right connector from last child*/
li:first-child::before, li:last-child::after{
	border: 0 none;
}
/*Adding back the vertical connector to the last nodes*/
li:last-child::before{
	border-right: 1px solid rgb(7, 5, 5);
	border-radius: 0 5px 0 0;
	-webkit-border-radius: 0 5px 0 0;
	-moz-border-radius: 0 5px 0 0;
}
li:first-child::after{
	border-radius: 5px 0 0 0;
	-webkit-border-radius: 5px 0 0 0;
	-moz-border-radius: 5px 0 0 0;
}

ul ul::before{
	content: '';
	position: absolute; top: 0; left: 50%;
	border-left: 1px solid rgb(7, 5, 5);
	width: 0; height: 20px;
}

</style>