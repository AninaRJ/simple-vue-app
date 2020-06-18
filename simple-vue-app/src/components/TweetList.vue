<template>
	<div class="tweet-list">
		<b-list-group v-for="tweetItem in tweets" v-bind:key="tweetItem.id">
			<TweetItem v-bind:tweetItem="tweetItem" v-if="tweetItem.is_quote_status" v-bind:quoteTweet="tweetItem.quoted_status"/>
			<TweetItem v-bind:tweetItem="tweetItem" v-else/>
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
	margin: auto;
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