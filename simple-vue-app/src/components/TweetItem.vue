<template>
	<b-list-group-item>
		<b-container>
			<b-row>
				<b-col sm="3">
					<b-media class="tweet-author-img">
						<template v-slot:aside>
							<b-img width="64" v-if="tweetItem.text.startsWith('RT')" rounded="circle" v-bind:src="tweetItem.retweeted_status.user.profile_image_url"></b-img>
							<b-img width="64" v-else rounded="circle" v-bind:src="tweetItem.user.profile_image_url"></b-img>
						</template>
					</b-media>
					<div class="tweet-author" v-if="tweetItem.text.startsWith('RT')">@{{tweetItem.retweeted_status.user.screen_name}}</div>
					<div class="tweet-author" v-else>@{{tweetItem.user.screen_name}}</div>
				</b-col>
				<b-col sm="9">
					<div class="tweet" v-if="tweetItem.text.startsWith('RT')">
						{{tweetItem.text.substring(tweetItem.text.indexOf(':') + 1)}}
					</div>
					<div class="tweet" v-else-if="tweetItem.text.startsWith('@')">
						<span v-for="(user, index) in tweetItem.entities.user_mentions" v-bind:key="user">
							<b-link>@{{user.screen_name}}</b-link>
							<span v-if="index < (tweetItem.entities.user_mentions.length -1)">&nbsp;</span>
						</span>
						{{tweetItem.text.split(tweetItem.entities.user_mentions[tweetItem.entities.user_mentions.length-1].screen_name)[1]}}
					</div>
					<div class="tweet" v-else>
						{{tweetItem.text}}
					</div>
					<b-link class="tweet-timestamp" v-if="tweetItem.text.startsWith('RT')">Retweeted by @{{tweetItem.user.screen_name}}</b-link>
				</b-col>
			</b-row>
		</b-container>
		<b-container>
			<b-media>
				<b-embed type="embed" v-if="tweetItem.entities.urls != undefined && tweetItem.entities.urls[0] != undefined" v-bind:src="tweetItem.entities.urls[0].url"/>
				<b-embed v-if="tweetItem.extended_entities != undefined && tweetItem.extended_entities.media != undefined" 
					type="embed" v-bind:src="tweetItem.extended_entities.media[0].video_info.variants[0].url"/>
			</b-media>
		</b-container>
		<b-container>
			<b-row align-content="center">
				<b-col align-self="center">
					<!-- RETWEET COUNT -->
					<b-button variant="link" v-if="tweetItem.retweeted">
						<b-icon icon="arrow-repeat" variant="success"/>&nbsp;
						<b-badge variant="success">{{tweetItem.retweet_count}}</b-badge>
					</b-button>
					<b-button variant="link" v-else>
						<b-icon icon="arrow-repeat" variant="info"/>&nbsp;
						<b-badge variant="info">{{tweetItem.retweet_count}}</b-badge>
					</b-button>
					<!-- FAVOURITE COUNT -->
					<b-button variant="link" v-if="tweetItem.favourited">
						<b-icon icon="heart-fill" variant="danger"/>&nbsp;
						<b-badge variant="info">{{tweetItem.favorite_count}}</b-badge>
					</b-button>
					<b-button variant="link" v-else>
						<b-icon icon="heart" variant="info"/>&nbsp;
						<b-badge variant="info">{{tweetItem.favorite_count}}</b-badge>
					</b-button>
				</b-col>
			</b-row>
		</b-container>
		<b-container>
			<b-row>
				<b-col>
					<span class="tweet-timestamp">{{new Date(tweetItem.created_at).toLocaleString()}}</span>
				</b-col>
			</b-row>
		</b-container>
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
	 text-align: center;
	 color: cadetblue;
	 font-weight: bold;
 }
 .tweet-timestamp{
	 font-size: 12px;
	 float: left;
	 width: fit-content;
	 font-weight: bold;
 }
 .tweet{
	 font-size: 18px;
	 text-align: start;
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