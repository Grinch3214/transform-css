<template>
	<div class="wrapper">
		<header class="header">
			<h1 class="header__title">
				Transform CSS Generator
			</h1>
		</header>

		<main class="main">
			<transform-generator />
		</main>

		<footer class="footer">
			<span>© 2023</span> | <a class="footer__link" href="https://github.com/" target="_blank">
				<icon-github />
				<span>GitHub</span>
			</a>
		</footer>
	</div>
</template>

<script>
import TransformGenerator from './components/TransformGenerator.vue'
import IconGithub from './components/icons/IconGithub.vue'

export default {
  components: { 
		TransformGenerator,
		IconGithub
	},
}
</script>

<style scoped>

</style>
