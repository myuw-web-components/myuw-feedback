# myuw-feedback

**`myuw-feedback` is not currently maintained.**

This component works similarily to the Help Dialog component, providing a way to present information in a dialog so users can take action quickly, without leaving the page. If dialog feels unnecessary, a quick link option is available.

## Getting started

Include the component on your page:

```html
<!-- import the module -->
<script type="module" src="https://cdn.my.wisc.edu/@myuw-web-components/myuw-feedback@latest/myuw-feedback.min.mjs"></script>

<!-- fallback for browsers without ES2015 module support -->
<script nomodule src="https://unpkg.com/@myuw-web-components/myuw-feedback@latest/myuw-feedback.min.js"></script>

<myuw-feedback
  myuw-feedback-title="Give feedback"
  show-button || show-link
>
  <!-- Option with Dialog -->
  <div class="your-div-here" slot="myuw-feedback-content">
    Your custom content
  </div>

  <!-- Option with link -->
    <div slot="myuw-feedback-link">
      <a id="myuw-feedback-link" aria-label="Open link to provide feedback" href="" target="_blank">
        <svg aria-hidden="true" id="feedback-icon" xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 0 24 24" width="24"><path d="M0 0h24v24H0z" fill="none"/><path d="M20 2H4c-1.1 0-1.99.9-1.99 2L2 22l4-4h14c1.1 0 2-.9 2-2V4c0-1.1-.9-2-2-2zm-7 12h-2v-2h2v2zm0-4h-2V6h2v4z"/></svg>
      </a>
    </div>
</myuw-feedback>
```

_Note:_ The evergreen "latest" version can be used for convenience, but in production settings it is recommended to use the latest [release version](https://github.com/myuw-web-components/myuw-feedback/releases) specifically, and upgrade only after testing!

### Trigger dialog

If you aren't using the top bar button (via the `show-button` attribute), fire the `show-myuw-feedback` event on the `document` when you want the dialog to display (e.g. when your "feedback" button is clicked):

```js
function showFeedbackDialog() {
  var event = new Event('show-myuw-feedback');
  document.dispatchEvent(event);
}
```

### Set up custom positioning

If you want to control the exact positioning of the dialog, you can dispatch a `CustomEvent` called `set-myuw-feedback-position` with position data like so:

```js
function showFeedbackDialog() {
  const event = new CustomEvent('show-myuw-feedback', {
    detail: { // required by CustomEvent spec
      position: { // "position" required by myuw-feedback component
        top: '100px', // "top" required by myuw-feedback component
        left: '100px', // "left" required by myuw-feedback component
      }
    }
  });
  document.dispatchEvent(event);
}
```

*Note: It is important that you use that exact event name and dispatch the event from the document scope. The component listens for the* `show-myuw-feedback`  *and* `set-myuw-feedback-position` *events.*

### Configurable properties via attributes

- **myuw-feedback-title**: The title to display at the top of the dialog
- **show-button**: Include this attribute if you want the icon button to appear the the top bar. If you want to trigger the dialog some other way, you're free to omit this attribute.
- **show-link**: Include this attribute if you want to pass an anchor tag, to provide a quick redirection to a Feedback mechanism of your choice.

### Slots

- **myuw-feedback-content**: Use this slot to insert your own content into the dialog (with whatever markup and styling you want).

## Development and contribution

To run the demo app locally and test the component, run the following commands:

```bash
$ npm install
$ npm start
```

Cross-browser testing provided by:<br/>
<a href="https://www.browserstack.com/"><img width="160" src="https://myuw-web-components.github.io/img/Browserstack-logo.svg" alt="BrowserStack"/></a>
