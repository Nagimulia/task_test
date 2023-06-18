<template>
	<nav class="main-nav">
		<router-link :to="{name:'home'}">
			Task
		</router-link>
		<router-link :to="{name:'addNewProject'}">
			Add New Deadline
		</router-link>
	

	</nav>
</template>

<style scoped>
.main-nav{
	text-align: center;
	margin: 40px 0;
}

.main-nav a{
	display: inline-block;
	text-decoration: none;
	margin: 0 10px;
	color: blueviolet;
	font-size: 25px;
}
a.router-link-active{
	border-bottom: 2px solid sandybrown;
	padding-bottom: 4px;
}
</style>