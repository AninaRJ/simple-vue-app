<template>
	<div class="profile-section">
		<b-list-group>
			<b-list-group-item>
				<b-img rounded="circle" width="84px" v-bind:src="profile.profile_image_url_https"/>
				<h4>{{profile.name}}</h4>
				<h5><b-link>@{{profile.screen_name}}</b-link></h5>
				<p>{{profile.description}}</p>
			</b-list-group-item>
			<b-list-group-item>
				<b-button variant="link">
					Followers <b-badge variant="info">{{profile.followers_count}}</b-badge>
				</b-button>
				<b-button variant="link">
					Following <b-badge variant="info">{{profile.friends_count}}</b-badge>
				</b-button>
				<b-button variant="link">
					Favourites <b-badge variant="info">{{profile.favourites_count}}</b-badge>
				</b-button>
			</b-list-group-item>
			<b-list-group-item>
				<p>User since: {{new Date(profile.created_at).toLocaleDateString("en-US", { year: 'numeric', month: 'long', day: 'numeric' })}}</p>
			</b-list-group-item>
		</b-list-group>
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
		width: 40%;
		float: right;
		text-align: center;
		margin: 37px;
	}

	.profile-section > .list-group > .list-group-item{
		background-color: bisque;
	}
</style>