<template>
	<b-navbar toggleable="lg" type="dark" variant="info">
		<b-navbar-brand href="#">
			Mock Twitter
		</b-navbar-brand>
		<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
		<b-collapse id="nav-collapse" is-nav>
			<!-- Right aligned nav items -->
			<b-navbar-nav class="ml-auto">
				<b-nav-form>
					<b-form-input id="search-user" size="sm" :state="search"  class="mr-sm-2" placeholder="Search"></b-form-input>
					<b-button size="sm" variant="dark" class="my-2 my-sm-0" type="button" @click="$emit('submit-search')">Search</b-button>
				</b-nav-form>
			</b-navbar-nav>
		</b-collapse>
	</b-navbar>
</template>

<script>
export default {
	name: 'Header'
}
</script>

<style scoped>

</style>