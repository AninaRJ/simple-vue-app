<template>
	<b-list-group-item class="flex-column align-items-start">
		<!-- Text and dp content -->
		<b-container>
			<b-row>
				<b-col sm="3">
					<b-media class="tweet-author-img">
						<template v-slot:aside>
							<b-img width="64" v-if="tweetItem.text.startsWith('RT')" rounded="circle" v-bind:src="tweetItem.retweeted_status.user.profile_image_url"></b-img>
							<b-img width="64" v-else rounded="circle" v-bind:src="tweetItem.user.profile_image_url"></b-img>

							<b-icon icon="chat-square-quote-fill" v-if="quoteTweet" variant="info"/>
						</template>
					</b-media>
					<small class="tweet-author" v-if="tweetItem.text.startsWith('RT')">@{{tweetItem.retweeted_status.user.screen_name}}</small>
					<small class="tweet-author" v-else>@{{tweetItem.user.screen_name}}</small>
				</b-col>
				<b-col sm="9">
					<div class="tweet" v-if="tweetItem.text.startsWith('RT')">
						{{tweetItem.text.substring(tweetItem.text.indexOf(':') + 1)}}
					</div>
					<div class="tweet" v-else-if="tweetItem.text.startsWith('@')">
						<span v-for="user in tweetItem.entities.user_mentions" v-bind:key="user">
							<b-button pill variant="warning" v-if="tweetItem.in_reply_to_screen_name == user.screen_name" size="sm" class="mb-2">
								<b-icon icon="reply-fill" flip-h aria-hidden="true"></b-icon>@{{user.screen_name}}
							</b-button>
						</span>
						<span v-for="(user, index) in tweetItem.entities.user_mentions" v-bind:key="user">
							<b-button pill variant="dark" v-if="tweetItem.in_reply_to_screen_name != user.screen_name && index == 1" size="sm" class="ml-1 mb-2">
								cc: @{{user.screen_name}}
								<b-badge variant="light" v-if="tweetItem.entities.user_mentions.length > 2">
									&nbsp;+ {{tweetItem.entities.user_mentions.length -2}}
								</b-badge>
							</b-button>
						</span>
						<div>
							{{tweetItem.text.split(tweetItem.entities.user_mentions[tweetItem.entities.user_mentions.length-1].screen_name)[1]}}
						</div>
					</div>
					<div class="tweet" v-else>
						{{tweetItem.text}}
					</div>
					<b-link class="tweet-timestamp" v-if="tweetItem.text.startsWith('RT')">Retweeted by @{{tweetItem.user.screen_name}}</b-link>
				</b-col>
			</b-row>
		</b-container>
		<b-container>
			<div v-if="quoteTweet">
				<TweetItem v-bind:tweetItem="quoteTweet"/>
			</div>
		</b-container>
		<!-- Video and embedded tweets -->
		<b-container>
			<b-media>
				<b-embed allowfullscreen aspect="21by9" type="video" v-if="tweetItem.entities.urls != undefined && tweetItem.entities.urls[0] != undefined && !quoteTweet" 
					v-bind:src="tweetItem.entities.urls[0].expanded_url"/>
				<b-embed v-if="tweetItem.extended_entities != undefined && tweetItem.extended_entities.media != undefined && !quoteTweet"
					type="video">
					<source v-bind:src="tweetItem.extended_entities.media[0].video_info.variants[0].url" 
						v-bind:type="tweetItem.extended_entities.media[0].video_info.variants[0].content_type">
				</b-embed>
			</b-media>
		</b-container>
		<!-- statistics content -->
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
	props: ['tweetItem', 'quoteTweet'],
	components:{
		TweetAction
	},
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