<template>
	<div class="tweet-section">
		<b-form-textarea rows="8" class="tweet-text-area" id="tweet" />
		<b-button variant="primary" value="tweet" @click="$emit('submit-tweet')">Tweet</b-button>
	</div>
</template>

<script>
export default {
	name: 'TweetTextArea'
}
</script>

<style scoped>
	.tweet-section{
		align-items: center;
		width: 40%;
		float: right;
		text-align: center;
		margin-top: 28px;
	}

	.tweet-text-area{
		width: 80%;
		font-size: 20px;
		font-family: inherit;
		margin: 10px;
	}
</style>