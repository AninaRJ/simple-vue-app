<template>
	<div class="tweet-list">
		<h4>Latest Tweets</h4>
		<b-list-group v-for="tweetItem in tweets" v-bind:key="tweetItem.id">
			<TweetItem v-bind:tweetItem="tweetItem"/>
		</b-list-group>
	</div>
</template>

<script>
import TweetItem from './TweetItem';
export default {
	name: 'TweetList',
	components: {
		TweetItem
	},
	props: ['tweets']
}
</script>

<style scoped>
.tweet-list{
	text-align: center;
	align-items: center;
	width: 50%;
	float: right;
}

.tweet-list h4{
	vertical-align: middle;
	margin: 5px;
}

.tweet-list ul{
	margin: 0px;
	padding: 0px;
}
</style>