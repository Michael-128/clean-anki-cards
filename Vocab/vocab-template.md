# Clean Vocab Template
## Setup
Copy the following HTML & CSS into your card template.

#### Optional
Install a custom font.
- Follow this [guide](https://docs.ankiweb.net/templates/styling.html#installing-fonts) to set up custom font in Anki
- Replace the font url in Style section
	- From: `@font-face { font-family: FontJP; src: url('_NotoSansJP-Regular.ttf'); }`
	- To: `@font-face { font-family: FontJP; src: url('_(your font file name)'); }`

I'm using [Noto Sans JP](https://fonts.google.com/noto/specimen/Noto+Sans+JP).

## Front Template
```html
<div id="frontSide">
	<div id="term">{{Term}}</div>
	<div id="sentence">{{Sentence}}</div>
</div>

<!-- Script below highlights the reviewed term in the sentence. It's entirely optional and can be removed. -->
<input id="input-term" type="hidden" value="{{Term}}">
<script>
	(function(){
		var word = document.querySelector("#input-term"); 
		var sentence = document.querySelector("#sentence");
		sentence.innerHTML = sentence.innerHTML.replaceAll(word.value,  "<span id='word-highlight'>"+word.value+"</span>")
	})();
</script>
```

## Back Template
```html
<div id="bothSides">
	{{FrontSide}}

	<div id="backSide">
		<div id="meaning">{{Meaning}}</div>
		<div id="pronounciation">
			<div id="graph">{{Graph}}</div>
			<div id="audio">{{Audio}}</div>
		</div>
		<div id="source">{{Source}}</div>
	</div>

	<!-- Displayed only if there is an actual screenshot -->
	{{#Screenshot}}
		<div id="screenshot">
			{{Screenshot}}
		</div>
	{{/Screenshot}}
</div>

<!-- Script below adds furigana to the reviewed term. It shouldn't be removed. -->
<input id="input-reading" type="hidden" value="{{Reading}}">
<script>
	(function(){
 		var word = document.querySelector("#term");
		var reading = document.querySelector("#input-reading");
		word.innerHTML = reading.value;
	})();
</script>

<!-- Script below adds spacing between the definitions. It's entirely optional and can be removed. -->
<script>
	(function(){
		var meaning = document.querySelector("#meaning");
		meaning.innerHTML = meaning.innerHTML.replaceAll("<br>", "<div class='br'></div>");
	})();
</script>
```

## Style
```css
@font-face { font-family: FontJP; src: url('_NotoSansJP-Regular.ttf'); }

.card {
	margin: 0;
	padding: 0;
	max-width: 800px;
	margin: auto;

	--border-radius: .25rem;
}

.card * {
	font-family: FontJP, sans-serif;
}

.card #frontSide, .card #backSide, .card #screenshot {
	background-color: rgba(0,0,0,0.1);

	border-radius: var(--border-radius);

	margin: 1rem;
	padding: 1rem;
}

.card.nightMode #frontSide, .card.nightMode #backSide, .card.nightMode #screenshot {
	background-color: rgba(255,255,255,0.05);
} 

.card #term {
	font-size: xx-large;
	text-align: center;
}

.card #sentence {
	font-size: large;
	text-align: center;
	color: rgba(0,0,0,0.8);
}

.card.nightMode #sentence {
	color: rgba(255,255,255,0.8);
}

.card #sentence #word-highlight {
	color: black;
	text-decoration: underline;
}

.card.nightMode #sentence #word-highlight {
	color: white;
}

.card #meaning {
	font-size: x-large;
}

.card #meaning .br {
	height: 1.5rem;
}

.card #meaning ul, .card #meaning ol {
	list-style-type: square;
	list-style-position: inside;

	width: fit-content;

	margin: auto;
	padding: 0;
}

.card #meaning ol {
	list-style-type: none;
}

.card #pronounciation {
	font-size: x-large;
	margin: 1rem;

	display: flex;
	justify-content: center;
}

.mobile .card #pronounciation {
	flex-direction: column;
	align-items: center;
}

.card #source {
	text-align: center;
	font-size: small;
}

.card #screenshot {
	text-align: center;
}

.card #screenshot img {
	border-radius: var(--border-radius);
}
```
