<template>
	<div>
		<ul class="tweet-action-list">
			<li>Delete</li>
			<li>Copy tweet</li>
		</ul>
	</div>
</template>

<script>
export default {
	name: 'TweetAction'
}
</script>

<style scoped>
	.tweet-action-list{
		list-style-type: none;
		width: max-content;
		float: right;
		display: block;
		border: 1px solid black;
		text-align: center;
		padding: 0px;
	}

	.tweet-action-list li{
		padding: 5px;
		font-size: bold;
	}

	.tweet-action-list li:hover{
		background-color: lightsalmon;
		cursor: pointer;
	}
</style>