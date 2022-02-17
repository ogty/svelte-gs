<script>
	import Nested1 from "./components/Nested1.svelte"           // Nested components
	import Nested2 from './components/Nested2.svelte'           // Declaring props
	import Nested3 from './components/Nested3.svelte'           // Default values
	import Info from './components/Info.svelte'                 // Spread props
	import Thing from './components/Thing.svelte'               // Keyed each blocks
	import Inner from './components/Inner.svelte'               // Component events
	import Outer from './components/Outer.svelte'               // Event forwading
	import CustomButton from './components/CustomButton.svelte' // DOM event forwarding
	// import { marked } from 'marked'                             // Textarea inputs
	import Media from "./components/Media.svelte"               // Media elements
	import { onMount } from 'svelte'                            // This
	import Keypad from './components/Keypad.svelte'             // Component bindings
	import InputField from './components/InputField.svelte'     // Binding to component instances


	// Basics
	let name = "world"

	// Adding data
	let src = "/images/img1.jpg"
	
	// HTML tags
	let string = `this string contains some <strong>HTML!!</strong>`

	// Assignments
	let count1 = 0;
	function incrementCount() {
		count1 += 1;
	}

	// Declarations
	let count2 = 0;
	$: doubled = count2 * 2;
	function handleClick() {
		count2 += 1;
	}

	// Statements
	let count3 = 0
	function handleClick2() {
		count3 += 1;
	}
	$: if (count3 >= 10) {
		alert('count is dangerously high!');
		count3 = 9;
	}

	// Updating arrays and objects
	let numbers = [1, 2, 3, 4];
	function addNumber() {
		numbers[numbers.length] = numbers.length + 1;
	}
	$: sum = numbers.reduce((t, n) => t + n, 0);

	// Spread props
	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};

	// If blocks and Else blocks
	let user = { loggedIn: false };
	function toggle() {
		user.loggedIn = !user.loggedIn;
	}

	// Else-if blocks
	let x = 7;

	// Each blocks
	let cats = [
		{ id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
	];

	// Keyed each blocks
	let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' },
	];

	function handleClick3() {
		things = things.slice(1);
	}

	// Await blocks
	async function getRandomNumber() {
		const res = await fetch(`/random-number`);
		const text = await res.text();

		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}

	let promise = getRandomNumber();

	function handleClick4() {
		promise = getRandomNumber();
	}

	// DOM events
	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

	// Inline handler
	let m2 = { x: 0, y: 0 };

	// Event modifiers
	function handleClick5() {
		alert('no more alerts')
	}

	// Component events
	function handleMessage(event) {
		alert(event.detail.text);
	}

	// Event forwading
	function handleMessage2(event) {
		alert(event.detail.text);
	}

	// DOM events forwading
	function handleClick6() {
		alert('Button Clicked');
	}

	// Text inputs
	let name2 = "world"

	// Numeric inputs
	let a = 1;
	let b = 2;

	// Checkbox inputs
	let yes = false;

	// Group inputs
	let scoops = 1;
	let flavours = ['Mint choc chip'];

	let menu = [
		'Cookies and cream',
		'Mint choc chip',
		'Raspberry ripple'
	];
	
	function join(flavours) {
		if (flavours.length === 1) return flavours[0];
		return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`;
	}

	// Textarea inputs
	let value = `Some words are *italic*, some are **bold**`;

	// Select bindings
	let questions = [
		{ id: 1, text: `Where did you go to school?` },
		{ id: 2, text: `What is your mother's name?` },
		{ id: 3, text: `What is another personal fact that an attacker could easily find with Google?` }
	];

	let selected;

	let answer = '';

	function handleSubmit() {
		alert(`answered question ${selected.id} (${selected.text}) with "${answer}"`);
	}

	// Select multiple
	let scoops2 = 1;
	let flavours2 = ['Mint choc chip'];

	let menu2 = [
		'Cookies and cream',
		'Mint choc chip',
		'Raspberry ripple'
	];

	function join2(flavours) {
		if (flavours.length === 1) return flavours[0];
		return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`;
	}

	// Contenteditable bindings
	let html = '<p>Write some text!</p>';

	// Each blocks bindings
	let todos = [
		{ done: false, text: 'finish Svelte tutorial' },
		{ done: false, text: 'build an app' },
		{ done: false, text: 'world domination' }
	];

	function add() {
		todos = todos.concat({ done: false, text: '' });
	}

	function clear() {
		todos = todos.filter(t => !t.done);
	}

	$: remaining = todos.filter(t => !t.done).length;

	// Dimensions
	let w;
	let h;
	let size = 42;
	let text = 'edit me';

	// This
	let canvas;

	onMount(() => {
		const ctx = canvas.getContext('2d');
		let frame = requestAnimationFrame(loop);

		function loop(t) {
			frame = requestAnimationFrame(loop);

			const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);

			for (let p = 0; p < imageData.data.length; p += 4) {
				const i = p / 4;
				const x = i % canvas.width;
				const y = i / canvas.width >>> 0;

				const r = 64 + (128 * x / canvas.width) + (64 * Math.sin(t / 1000));
				const g = 64 + (128 * y / canvas.height) + (64 * Math.cos(t / 1000));
				const b = 128;

				imageData.data[p + 0] = r;
				imageData.data[p + 1] = g;
				imageData.data[p + 2] = b;
				imageData.data[p + 3] = 255;
			}

			ctx.putImageData(imageData, 0, 0);
		}

		return () => {
			cancelAnimationFrame(frame);
		};
	});

	// Component bindings
	let pin;
	$: view = pin ? pin.replace(/\d(?!$)/g, '•') : 'enter your pin';

	function handleSubmit2() {
		alert(`submitted ${pin}`);
	}

	// Binding to component instances
	let field
</script>

<!-- Basics -->
<h1>Hello world!</h1>
<hr>

<!-- Adding data -->
<h2>Hello {name.toLocaleLowerCase()}!</h2>
<ul>
	<li>toLocaleLowerCase</li>
	<li>toLocaleUpperCase</li>
	<li>toLowerCase</li>
	<li>toString</li>
	<li>toUpperCase</li>
</ul>

<!-- Dynamic attributes -->
<img {src} alt="img1" width="50px" height="50px">
<hr>

<!-- Styling -->
<p>This is a paragraph.</p>

<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
	div { width: 100%; height: 100%; }
	label { display: flex }
	input, p { margin: 6px }
	textarea { width: 100%; height: 200px; }
	input {
		display: block;
		width: 500px;
		max-width: 100%;
	}
	[contenteditable] {
		padding: 0.5em;
		border: 1px solid #eee;
		border-radius: 4px;
	}
	canvas {
		width: 100%;
		height: 100%;
		background-color: #666;
		-webkit-mask: url(/svelte-logo-mask.svg) 50% 50% no-repeat;
		mask: url(/svelte-logo-mask.svg) 50% 50% no-repeat;
	}
</style>

<p>This is a paragraph.</p>
<hr>

<!-- Nested components -->
<p>This is a paragraph.</p>
<Nested1/>
<hr>

<!-- HTML tags -->
<p>{@html string}</p>
<hr>

<!-- Assignments -->
<button on:click={incrementCount}>
	Clicked {count1} {count1 === 1 ? 'time' : 'times'}
</button>
<hr>

<!-- Declarations -->
<button on:click={handleClick}>
	Clicked {count2} {count2 === 1 ? 'time' : 'times'}
</button>

<p>{count2} doubled is {doubled}</p>
<hr>

<!-- Statements -->
<button on:click={handleClick2}>
	Clicked {count3} {count3 === 1 ? 'time' : 'times'}
</button>
<hr>

<!-- Updating arrays and objects -->
<p>{numbers.join(' + ')} = {sum}</p>

<button on:click={addNumber}>
	Add a number
</button>
<hr>

<!-- Declaring props -->
<Nested2 answer={42}/>
<hr>

<!-- Default values -->
<Nested3 answer={42}/>
<Nested3/>
<hr>

<!-- Spread props -->
<Info name={pkg.name} version={pkg.version} speed={pkg.speed} website={pkg.website}/>
<hr>

<!-- If blocks -->
{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{/if}

{#if !user.loggedIn}
	<button on:click={toggle}>
		Log in
	</button>
{/if}
<hr>

<!-- Else blocks -->
{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{:else}
	<button on:click={toggle}>
		Log in
	</button>
{/if}
<hr>

<!-- Else-if blocks -->
{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}
<hr>

<!-- Each blocks -->
<h1>The Famous Cats of YouTube</h1>

<ul>
{#each cats as cat, i}
	<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
		{i + 1}: {cat.name}
	</a></li>
{/each}
</ul>
<hr>

<!-- Keyed each blocks -->
<button on:click={handleClick3}>
	Remove first thing
</button>

{#each things as thing (thing.id) }
	<Thing name={thing.name}/>
{/each}
<hr>

<!-- Await blocks -->
<button on:click={handleClick4}>
	generate random number
</button>

{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

{#await promise then value}
	<p>the value is {value}</p>
{/await}
<hr>

<!-- DOM events -->
<div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div>
<hr>

<!-- Inline handlers -->
<div on:mousemove="{e => m2 = { x: e.clientX, y: e.clientY }}">
	The mouse position is {m2.x} x {m2.y}
</div>
<hr>

<!-- Event modifiers -->
<button on:click|once={handleClick5}>
	Click me
</button>
<ul>
	<li>preventDefault — ハンドラを実行する前に event.preventDefault() を呼び出します。たとえば、クライアントのフォーム処理に役立ちます。</li>
	<li>stopPropagation — 次の要素にイベントが伝播しないように event.stopPropagation() を呼び出します。</li>
	<li>passive — タッチ/ホイールイベントでスクロールのパフォーマンスを向上させます（Svelte が安全な場所に自動的に追加します）。</li>
	<li>nonpassive — passive: false を明示的に設定します。</li>
	<li>capture — バブリング フェーズではなく、キャプチャ フェーズ中にハンドラを起動します。(MDN docs)</li>
	<li>once — ハンドラを最初に実行した後に削除します。</li>
	<li>self — 設定した要素が event.target の場合にのみ、ハンドラをトリガします。</li>
	<li>trusted — event.isTrusted が true の場合にのみハンドラをトリガします。つまり、ユーザーのアクションによってイベントがトリガされた場合です。</li>
	<li>イベント修飾子を連結することができます。（例）pre>on:click|once|capture=</li>
</ul>
<hr>

<!-- Component events -->
<Inner on:message={handleMessage}/>
<hr>

<!-- Event forwarding -->
<Outer on:message={handleMessage2}/>
<hr>

<!-- DOM events forwarding -->
<CustomButton on:click={handleClick6}/>
<hr>

<!-- Text inputs -->
<input bind:value={name}>

<h1>Hello {name}!</h1>
<hr>

<!-- Numeric inputs -->
<label>
	<input type=number bind:value={a} min=0 max=10>
	<input type=range bind:value={a} min=0 max=10>
</label>

<label>
	<input type=number bind:value={b} min=0 max=10>
	<input type=range bind:value={b} min=0 max=10>
</label>

<p>{a} + {b} = {a + b}</p>
<hr>

<!-- Checkbox inputs -->
<label>
	<input type=checkbox bind:checked={yes}>
	Yes! Send me regular email spam
</label>

{#if yes}
	<p>Thank you. We will bombard your inbox and sell your personal details.</p>
{:else}
	<p>You must opt in to continue. If you're not paying, you're the product.</p>
{/if}

<button disabled={!yes}>
	Subscribe
</button>
<hr>

<!-- Group inputs -->
<h2>Size</h2>

<label>
	<input type=radio bind:group={scoops} name="scoops" value={1}>
	One scoop
</label>

<label>
	<input type=radio group={scoops} name="scoops" value={2}>
	Two scoops
</label>

<label>
	<input type=radio group={scoops} name="scoops" value={3}>
	Three scoops
</label>

<h2>Flavours</h2>

{#each menu as flavour}
	<label>
		<input type=checkbox bind:group={flavours} name="flavours" value={flavour}>
		{flavour}
	</label>
{/each}

{#if flavours.length === 0}
	<p>Please select at least one flavour</p>
{:else if flavours.length > scoops}
	<p>Can't order more flavours than scoops!</p>
{:else}
	<p>
		You ordered {scoops} {scoops === 1 ? 'scoop' : 'scoops'}
		of {join(flavours)}
	</p>
{/if}
<hr>

<!-- Textarea inputs -->
<!-- {@html marked(value)} -->

<textarea bind:value></textarea>
<hr>

<!-- Select bindings -->
<h2>Insecurity questions</h2>

<form on:submit|preventDefault={handleSubmit}>
	<select bind:value={selected} on:change="{() => answer = ''}">
		{#each questions as question}
			<option value={question}>
				{question.text}
			</option>
		{/each}
	</select>

	<input bind:value={answer}>

	<button disabled={!answer} type=submit>
		Submit
	</button>
</form>

<p>selected question {selected ? selected.id : '[waiting...]'}</p>
<hr>

<!-- Select multiple -->
<h2>Size</h2>

<label>
	<input type=radio bind:group={scoops2} value={1}>
	One scoop
</label>

<label>
	<input type=radio bind:group={scoops2} value={2}>
	Two scoops
</label>

<label>
	<input type=radio bind:group={scoops2} value={3}>
	Three scoops
</label>

<h2>Flavours</h2>

<select multiple bind:value={flavours2}>
	{#each menu2 as flavour}
		<option value={flavour}>
			{flavour}
		</option>
	{/each}
</select>

{#if flavours2.length === 0}
	<p>Please select at least one flavour</p>
{:else if flavours2.length > scoops2}
	<p>Can't order more flavours than scoops!</p>
{:else}
	<p>
		You ordered {scoops2} {scoops2 === 1 ? 'scoop' : 'scoops'}
		of {join2(flavours2)}
	</p>
{/if}
<hr>

<!-- Contenteditable bindings -->
<div
	contenteditable="true"
	bind:innerHTML={html}
></div>

<pre>{html}</pre>
<hr>

<!-- Each block bindings -->
<h1>Todos</h1>

{#each todos as todo}
	<input
		type=checkbox
		bind:checked={todo.done}
	>

	<input
		placeholder="What needs to be done?"
		bind:value={todo.text}
	>
{/each}

<p>{remaining} remaining</p>

<button on:click={add}>
	Add new
</button>

<button on:click={clear}>
	Clear completed
</button>
<hr>

<!-- Media elements -->
<Media />
<hr>

<!-- Dimenstions -->
<input type=range bind:value={size}>
<input bind:value={text}>

<p>size: {w}px x {h}px</p>

<div bind:clientWidth="{w}" bind:clientHeight="{h}">
  <span style="font-size: {size}px">{text}</span>
</div>
<hr>

<!-- This -->
<canvas
	bind:this={canvas}
	width={32}
	height={32}
></canvas>
<hr>

<!-- Component bindings -->
<h1 style="color: {pin ? '#333' : '#ccc'}">{view}</h1>

<Keypad bind:value={pin} on:submit={handleSubmit2}/>
<hr>

<!-- Binding to component instances -->
<InputField bind:this={field} />

<button on:click="{() => field.focus()}">
	Focus field
</button>
