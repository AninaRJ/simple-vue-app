<template>
	<b-list-group-item>
		<span class="tweet-author">@{{tweetItem.user.screen_name}}</span>
		<div class="tweet">{{tweetItem.text}}</div>
		<b-media class="tweet-author-img">
			<template v-slot:aside>
				<b-img width="64" rounded="circle" v-bind:src="tweetItem.user.profile_image_url"></b-img>
			</template>
		</b-media>
		<b-media>
			<b-embed type="embed" v-if="tweetItem.entities.urls != undefined && tweetItem.entities.urls[0] != undefined" v-bind:src="tweetItem.entities.urls[0].url"/>
			<b-embed v-if="tweetItem.extended_entities != undefined && tweetItem.extended_entities.media != undefined" 
				type="video" v-bind:src="tweetItem.extended_entities.media[0].video_info.variants[0].url"/>
		</b-media>
		<span class="tweet-timestamp">{{tweetItem.created_at}}</span>
	</b-list-group-item>
</template>

<script>
import TweetAction from './TweetAction.vue';
export default {
	name: 'TweetItem',
	props: ['tweetItem'],
	components:{
		TweetAction
	}
}
</script>

<style scoped>
 .tweet-author-img{
	 padding-bottom: 8px;
	 display: grid;
 }
 .tweet-author{
	 font-size: 14px;
	 float: left;
	 width: fit-content;
	 color: cadetblue;
 }
 .tweet-timestamp{
	 font-size: 12px;
	 float: left;
	 width: fit-content;
 }
 .tweet{
	 font-size: 20px;
	 text-align: end;
 }
 .hastag{
	 color: blue;
 }
 .tweet-action{
	 display: inline;
	 float: right;
 }
.tweet-action img{
	float: right;
}
.tweet-action img:hover{
	cursor: pointer;
}
.tweet-action-window{
	float: right;
}
</style>