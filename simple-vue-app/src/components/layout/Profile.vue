<template>
	<div class="profile-section">
		<b-list-group>
			<b-list-group-item variant="warning">
				<b-img rounded="circle" width="84px" v-bind:src="profile.profile_image_url_https"/>
				<h4>{{profile.name}}</h4>
				<h5><b-link>@{{profile.screen_name}}</b-link></h5>
				<p>{{profile.description}}</p>
			</b-list-group-item>
			<b-list-group-item variant="info">
				<b-button variant="link">
					Followers <b-badge variant="info">{{profile.followers_count}}</b-badge>
				</b-button>
				<b-button variant="link">
					Following <b-badge variant="info">{{profile.friends_count}}</b-badge>
				</b-button>
				<b-button variant="link">
					<b-icon icon="heart-fill" variant="danger"/>&nbsp;<b-badge variant="info">{{profile.favourites_count}}</b-badge>
				</b-button>
			</b-list-group-item>
			<b-list-group-item variant="warning"> 
				<p><b-icon icon="calendar-3"/>&nbsp;User since: {{new Date(profile.created_at).toLocaleDateString("en-US", { year: 'numeric', month: 'long', day: 'numeric' })}}</p>
			</b-list-group-item>
		</b-list-group>
		<!-- <b-carousel id="carousel-1" v-model="slide" :interval="4000" controls indicators background="#ababab" img-width="1024" img-height="480" style="text-shadow: 1px 1px 2px #333;"
			@sliding-start="onSlideStart"
			@sliding-end="onSlideEnd">
			<b-carousel-slide
				caption="First slide"
				text="Nulla vitae elit libero, a pharetra augue mollis interdum."
				img-src="https://picsum.photos/1024/480/?image=52"
      		>
			</b-carousel-slide>
    	</b-carousel> -->
	</div>
</template>

<script>
export default {
	name: 'Profile',
	props: ['profile']
}
</script>

<style scoped>
	.profile-section{
		align-items: center;
		text-align: center;
		margin: auto;
	}

	.profile-section > .list-group > .list-group-item{
	}
</style>