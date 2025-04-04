# DNA Interactive Visualization

An interactive 3D visualization of DNA structure and base pairs, designed for embedding in online textbooks.

## Features

- 3D visualization of DNA structure
- Interactive highlighting of base pairs (A-T, C-G)
- Toggle between linear and helix views
- Responsive design that works on all devices
- Easy to embed in any web page

## Embedding Instructions

There are two ways to embed this interactive:

### Option 1: Using the Smart Phrase

1. Open the `smart-phrase.html` file
2. Copy everything between the `<!-- DNA Interactive Smart Phrase - START -->` and `<!-- DNA Interactive Smart Phrase - END -->` comments
3. In your textbook's HTML editor, paste the code where you want the interactive to appear
4. The interactive will be automatically inserted with all necessary styling and functionality

The smart phrase includes:
- Introductory text explaining the DNA bases
- Interactive controls for viewing the DNA structure
- The 3D visualization
- All necessary JavaScript for interactivity

### Option 2: Manual Embedding

If you prefer to copy the code directly, you can use this version:

```html
<div class="dna-interactive-container" style="font-family: inherit; line-height: 1.6; margin: 20px 0; max-width: 800px; margin: 0 auto;">
    <p>
        DNA is composed of four types of nitrogenous bases: 
        <a href="#" class="dna-base-link" data-base="A" style="color: inherit; text-decoration: underline; cursor: pointer;">Adenine</a>, 
        <a href="#" class="dna-base-link" data-base="T" style="color: inherit; text-decoration: underline; cursor: pointer;">Thymine</a>, 
        <a href="#" class="dna-base-link" data-base="C" style="color: inherit; text-decoration: underline; cursor: pointer;">Cytosine</a>, and 
        <a href="#" class="dna-base-link" data-base="G" style="color: inherit; text-decoration: underline; cursor: pointer;">Guanine</a>.
    </p>

    <div class="dna-controls" style="margin: 10px 0; display: flex; gap: 10px; align-items: center;">
        <div id="dna-info" class="dna-info" style="background-color: rgba(0, 0, 0, 0.5); color: white; padding: 10px; border-radius: 5px; flex-grow: 1;">DNA Base Pairs</div>
        <button id="dna-view-toggle" class="dna-view-toggle" style="padding: 5px 15px; background-color: white; border: 1px solid #ccc; border-radius: 3px; cursor: pointer;">Helix Mode</button>
    </div>

    <iframe id="dna-visualization" class="dna-iframe" src="https://adriansalmoninteractives.github.io/dna-inline/" style="width: 100%; height: 600px; border: none; margin: 10px 0; background-color: transparent;"></iframe>

    <script>
        (function() {
            document.getElementById('dna-visualization').addEventListener('load', function() {
                document.querySelectorAll('.dna-base-link').forEach(link => {
                    link.addEventListener('mouseenter', function(e) {
                        e.preventDefault();
                        const base = this.dataset.base;
                        const iframe = document.getElementById('dna-visualization');
                        iframe.contentWindow.postMessage({
                            type: 'hover',
                            base: base
                        }, '*');
                    });
                    link.addEventListener('click', function(e) {
                        e.preventDefault();
                    });
                });
                document.getElementById('dna-view-toggle').addEventListener('click', function() {
                    const iframe = document.getElementById('dna-visualization');
                    iframe.contentWindow.postMessage({
                        type: 'toggleView'
                    }, '*');
                });
            });
        })();
    </script>
</div>
```

### Usage Notes

1. The interactive will automatically adapt to your page's font family and styling
2. The visualization is responsive and will resize to fit the container width
3. The height is set to 600px by default but can be adjusted by modifying the iframe's height style
4. The interactive supports both mouse and touch interactions
5. The base pair highlighting works by hovering over the base names above the visualization

## Technical Details

This interactive is built using Three.js for 3D rendering and is hosted on GitHub Pages. The visualization is embedded using an iframe with postMessage communication for interactivity.

## License

This project is open source and available under the MIT License.
