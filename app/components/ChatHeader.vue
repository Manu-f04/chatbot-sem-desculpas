<template>
	<header class="chat-header">
		<div class="chat-header__info">
			<div class="chat-header__avatar-wrapper">
				<img
					src="/foco.jpg"
					alt="Imagem do chatbot"
					class="chat-header__image"
				/>
				<span class="chat-header__status-dot" title="Online"></span>
			</div>

			<div class="chat-header__text">
				<div class="chat-header__title-row">
					<h1 class="chat-header__title">{{ title }}</h1>
					<span class="chat-header__status-badge">Online</span>
				</div>

				<p v-if="subtitle" class="chat-header__subtitle">
					{{ subtitle }}
				</p>
			</div>
		</div>
		<slot name="actions" />
	</header>
</template>

<script setup>
defineProps({
	title: {
		type: String,
		default: 'SEM DESCULPAS',
	},
	subtitle: {
		type: String,
		default: 'Seu choque de realidade diário.',
	},
})
</script>

<style scoped>
.chat-header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 1rem;
	padding: 1rem;
	border-bottom: 1px solid #333333;
	background: #1b1b1b;
}

.chat-header__info {
	display: flex;
	align-items: center;
	gap: 12px;
}

.chat-header__avatar-wrapper {
	position: relative;
	width: 50px;
	height: 50px;
	flex-shrink: 0;
}

.chat-header__image {
	width: 100%;
	height: 100%;
	object-fit: cover;
	border-radius: 50%;
	border: 2px solid #ff3434;
}

.chat-header__status-dot {
	position: absolute;
	bottom: 1px;
	right: 1px;
	width: 12px;
	height: 12px;
	background-color: #22c55e;
	border: 2px solid #1b1b1b;
	border-radius: 50%;
}

.chat-header__text {
	display: flex;
	flex-direction: column;
	gap: 4px;
}

.chat-header__title-row {
	display: flex;
	align-items: center;
	gap: 8px;
}

.chat-header__title {
	margin: 0;
	color: #ffffff;
	font-size: 1.125rem;
	font-weight: 800;
}

.chat-header__status-badge {
	font-size: 0.7rem;
	font-weight: 700;
	color: #22c55e;
	background-color: rgba(34, 197, 94, 0.12);
	border: 1px solid rgba(34, 197, 94, 0.3);
	padding: 2px 8px;
	border-radius: 999px;
}

.chat-header__subtitle {
	margin: 0;
	color: #aaaaaa;
	font-size: 0.875rem;
}

@media (max-width: 480px) {
	.chat-header {
		padding: 12px;
	}

	.chat-header__avatar-wrapper {
		width: 42px;
		height: 42px;
	}

	.chat-header__title {
		font-size: 1rem;
	}

	.chat-header__subtitle {
		font-size: 0.75rem;
	}
}
</style>