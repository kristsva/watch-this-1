<script>
	import LoadingIndicator from './Loading.svelte';

	/**
	 * @type string
	 */
	export let cinemaType;
	/**
	 * @type Array<string>
	 */
	export let selectedCategories;
	/**
	 * @type string
	 */
	export let specificDescriptors;
	/**
	 * @type Boolean
	 */
	export let loading;

	const categoryTypes = [
		'Akšons',
		'Piedzīvojumi',
		'Animācija',
		'Biogrāfija',
		'Komēdija',
		'Kriminaļņiks',
		'Dokumentālā',
		'Drāma',
		'Ģimenes',
		'Fantāzija',
		'Film-Noir',
		'Vēsturiska',
		'Šausmene',
		'Mūzikls',
		'Mistērija',
		'Romantika',
		'Sci-Fi',
		'Sports',
		'Trilleris',
		'Karš',
		'Vesterna',
		'Art-house',
		'Melnais humors',
		'Chick-flick',
		'Cult-classic',
		'Melnais humors',
		'Episkās',
		'Erotika',
		'Eksperimentāli',
		'Pasakas',
		'Filma filmā',
		'Futūristiska',
		'Gangsteru',
		'Laupīšana',
		'Vēsturiska',
		'Brīvdienu',
		'Indie',
		'Jauniešu',
		'Melodrāma',
		'Briesmoņu',
		'Politiska',
		'Psiholoģiska',
		'Filmas pa ceļam',
		'Satīrs',
		'Sci-Fi',
		'Slapstick',
		'Sabiedriskās problēmas',
		'Supervaroņi',
		'Sireālas',
		'Pusaudžu',
		'Vampīri',
		'Zombiji'
	];

	let cinemaTypes = [
		{ value: 'tv show', title: 'TV seriālu' },
		{ value: 'movie', title: 'Filmu' },
		{ value: 'tv show or movie', title: 'Man vienalga' }
	];
</script>

<div class="col-12">
	<div>
		<div class="mb-8">
			<div class="mb-2 font-semibold text-lg">Es gribu skatīties:</div>
			<div class="flex items-center">
				{#each cinemaTypes as type (type.value)}
					<button
						on:click={() => {
							cinemaType = type.value;
						}}
						class={`${
							cinemaType === type.value ? 'bg-red-600/40' : ''
						} text-slate-200 font-normal mr-3 text-sm mt-3 py-2 px-4 border border-red-600`}
					>
						{type.title}
					</button>
				{/each}
			</div>
		</div>
		<div>
			<div class="mb-4 font-semibold text-lg">
				Atķeksē savus mīļākos TV seriālu un/vai filmu žanrus:
			</div>
			<div class="flex items-center flex-wrap">
				{#each categoryTypes as category}
					<label
						class={`${
							selectedCategories.includes(category) ? 'bg-red-600/40' : ''
						} text-slate-200 font-normal mr-3 mt-3 text-sm py-2 px-4 border border-red-600`}
					>
						<input
							class="hidden"
							type="checkbox"
							bind:group={selectedCategories}
							name="categories"
							value={category}
						/>
						{category}
					</label>
				{/each}
			</div>
		</div>
		<div class="mt-8">
			<div class="mb-4 font-semibold text-lg">Tavs komentārs:</div>
			<textarea
				bind:value={specificDescriptors}
				class="textAreaField bg-white/40 border border-white/0 p-2 placeholder:text-slate-600 text-slate-900 w-full font-medium"
				placeholder="Piemēram, jābūt vismaz divām sezonām un jābūt Netflix un Hulu."
			/>
			<button
				on:click
				class={`${
					loading
						? 'bg-red-400/50'
						: 'generateBtn bg-red-600 hover:bg-gradient-to-r from-red-700 via-red-600 to-red-700 '
				} mt-4 w-full text-white font-bold p-3 flex items-center justify-center`}
			>
				{#if loading}
					<LoadingIndicator />
				{:else}
					<p>MEKLĒT</p>
				{/if}
			</button>
		</div>
	</div>
</div>

<style>
	label {
		cursor: pointer;
	}
	.generateBtn p {
		display: flex;
		align-items: center;
		justify-content: center;
		margin: 0 !important;
	}
	button {
		font-size: 12px !important;
	}
	textarea {
		min-height: 120px;
	}
	textarea::placeholder {
		font-weight: normal;
		color: #333 !important;
	}
	@media (max-width: 575px) {
		button {
			font-size: 11px !important;
		}
		label {
			font-size: 11px !important;
		}
	}
</style>
