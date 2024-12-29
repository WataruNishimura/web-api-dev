<script lang="ts" module>
	const templateElement = document.createElement('template');
	const slotElement = document.createElement('slot');

	const wrapperElement = document.createElement('span');
	wrapperElement.id = 'animate-target';
	wrapperElement.innerHTML = slotElement.outerHTML;

	templateElement.innerHTML = `
    <style>
      :host {
        white-space: nowrap;
        margin: 0 calc(50% - 50vw);
        width: 100vw;
        position: relative;
      }

      span {
        position: absolute;
        left: 100vw;
      }

      span::slotted(*) {
        position: relative;
        display: inline-block;
      }
    </style>
  `;

	class MarqueeX extends HTMLElement {
		speed: number;

		constructor() {
			super();
			this.attachShadow({ mode: 'open' });
			if (this.shadowRoot) {
				this.shadowRoot.appendChild(templateElement.content.cloneNode(true));
				this.shadowRoot.appendChild(wrapperElement);
			}

			const speedAttribute = this.getAttribute('speed');

			this.speed = speedAttribute ? parseInt(speedAttribute) : 5;
		}

		connectedCallback() {
			const animateTarget = this.shadowRoot?.getElementById('animate-target');
			if (animateTarget) {
				const keyframes = [{ left: '100vw' }, { left: '0' }];

				const options = {
					duration: window.innerWidth ? (window.innerWidth / this.speed) * 250 : 10000,
					iterations: Infinity
				};
				animateTarget.animate(keyframes, options);
			}
		}
	}
	window.customElements.define('marquee-x', MarqueeX);
</script>

<marquee-x speed="5"> Hello </marquee-x>
