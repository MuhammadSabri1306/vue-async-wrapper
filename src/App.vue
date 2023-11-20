<script setup>
import { AsyncWrapper, AsyncManualWrapper, AsyncSetupWrapper } from "./AsyncWrapper";

const loaderTestBasic = () => import("./components/TestBasic.vue");
const loaderTestManualResolve = () => import("./components/TestManualResolve.vue");
const loaderTestAsyncSetup = () => import("./components/TestAsyncSetup.vue");
</script>

<template>
	<header>
		<a href="https://vuejs.org/" target="_blank">
			<img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
		</a>
		<h3>Vue Async Wrapper</h3>
	</header>
	<main>
		<div class="component-wrapper">
			<h6>Test Basic Resolve</h6>
			<AsyncWrapper :loader="loaderTestBasic">
				<template #loading>
					<div class="card-status">
						<span>Loading component..</span>
					</div>
				</template>
				<template #error>
					<div class="card-status card-status-error">
						<span>Failed to loading component.</span>
					</div>
				</template>
			</AsyncWrapper>
		</div>

		<div class="component-wrapper">
			<h6>Test Manual Resolve</h6>
			<AsyncManualWrapper :loader="loaderTestManualResolve">
				<template #loading>
					<div class="card-status">
						<span>Loading component..</span>
					</div>
				</template>
				<template #error>
					<div class="card-status card-status-error">
						<span>Failed to loading component.</span>
					</div>
				</template>
			</AsyncManualWrapper>
		</div>

		<div class="component-wrapper">
			<h6>Test Manual Error</h6>
			<AsyncManualWrapper :loader="loaderTestManualResolve" isReject>
				<template #loading>
					<div class="card-status">
						<span>Loading component..</span>
					</div>
				</template>
				<template #error>
					<div class="card-status card-status-error">
						<span>Failed to loading component.</span>
					</div>
				</template>
			</AsyncManualWrapper>
		</div>

		<div class="component-wrapper">
			<h6>Test Async Setup Resolve</h6>
			<AsyncSetupWrapper :loader="loaderTestAsyncSetup">
				<template #loading>
					<div class="card-status">
						<span>Loading component..</span>
					</div>
				</template>
				<template #error>
					<div class="card-status card-status-error">
						<span>Failed to loading component.</span>
					</div>
				</template>
			</AsyncSetupWrapper>
		</div>

		<div class="component-wrapper">
			<h6>Test Async Setup Error</h6>
			<AsyncSetupWrapper :loader="loaderTestAsyncSetup" isReject>
				<template #loading>
					<div class="card-status">
						<span>Loading component..</span>
					</div>
				</template>
				<template #error>
					<div class="card-status card-status-error">
						<span>Failed to loading component.</span>
					</div>
				</template>
			</AsyncSetupWrapper>
		</div>
	</main>
</template>

<style scoped>
.logo {
	height: 6em;
	padding: 1.5em;
	will-change: filter;
	transition: filter 300ms;
}

.logo:hover {
	filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
	filter: drop-shadow(0 0 2em #42b883aa);
}

header {
	display: flex;
	justify-content: center;
	align-items: center;
}

header h3 {
	margin: 0;
	color: #424242;
}

main {
	padding: 1rem 10rem;
}

.component-wrapper {
	padding: 2rem;
	background-color: #f6f6f6;
	margin-bottom: 4rem;
	overflow: hidden;
}

.card-status {
	display: flex;
	justify-content: center;
	align-items: center;
	border: 1px solid #999;
	padding: 2rem 1rem;
}

.card-status span {
	text-align: center;
	font-weight: 600;
	font-size: .89rem;
	color: #424242;
}

.card-status-error {
	border: 1px solid #b45c5c;
	background-color: #ff9595;
}

.card-status-error span {
	color: #cd1818;
}
</style>
