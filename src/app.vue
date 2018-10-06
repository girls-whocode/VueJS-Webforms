<script>
import appConfig from '@src/app.config'

export default {
  page: {
    // All subcomponent titles will be injected into this template.
    titleTemplate(title) {
      title = typeof title === 'function' ? title(this.$store) : title
      return title ? `${title} | ${appConfig.title}` : appConfig.title
    },
  },
}
</script>

<template>
  <div id="app">
    <!--
    Even when routes use the same component, treat them
    as distinct and create the component again.
    -->
    <router-view :key="$route.fullPath" />
  </div>
</template>

<!-- This should generally be the only global CSS in the app. -->
<style lang="scss">
// Allow element/type selectors, because this is global CSS.
// stylelint-disable selector-max-type, selector-class-pattern

// Normalize default styles across browsers,
// https://necolas.github.io/normalize.css/
@import '~normalize.css/normalize.css';
// Style loading bar between pages.
// https://github.com/rstacruz/nprogress
@import '~nprogress/nprogress.css';

// Design variables and utilities from src/design.
@import '@design';

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  background: $color-body-bg;
}

#app {
  @extend %typography-small;
}

// ===
// Base element styles
// ===

a,
a:visited {
  color: $color-link-text;
}

h1 {
  @extend %typography-xxlarge;
}

h2 {
  @extend %typography-xlarge;
}

h3 {
  @extend %typography-large;
}

h4 {
  @extend %typography-medium;
}

h5,
h6 {
  @extend %typography-small;
}

.user-forms {
  margin-top: 25px;
}

.form-label-group {
  position: relative;
  margin-bottom: 1rem;
}

.form-label-group > input,
.form-label-group > label,
.form-label-group > select,
.form-label-group > textarea {
  padding: var(--input-padding-y) var(--input-padding-x);
}

.form-label-group input::-webkit-input-placeholder {
  color: transparent;
}

.form-label-group input:-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-moz-placeholder {
  color: transparent;
}

.form-label-group input::placeholder {
  color: transparent;
}

.form-label-group textarea::-webkit-input-placeholder {
  color: transparent;
}

.form-label-group textarea:-ms-input-placeholder {
  color: transparent;
}

.form-label-group textarea::-ms-input-placeholder {
  color: transparent;
}

.form-label-group textarea::-moz-placeholder {
  color: transparent;
}

.form-label-group textarea::placeholder {
  color: transparent;
}

/* - FIREFOX & CHROME
  Input Box Label
*/
.form-label-group > label {
  position: absolute;
  top: 0;
  left: 0;
  display: block;
  width: 100%;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 1.5;
  color: #aaa;
  border: 1px solid transparent;
  border-radius: 0.25rem;
  transition: all 0.1s ease-in-out;
}

/* - INTERNET EXPLORER
  Input Box Label
*/
.form-label-group > label {
  @media screen and (min-width:0\0) {
    margin-top: 8px !important;
    margin-left: 10px !important;
  }
}

/* - FIREFOX
  Input Box
*/
.form-label-group input:not(:placeholder-shown) {
  padding-top: calc(var(--input-padding-y) + var(--input-padding-y) * (2 / 3));
  padding-bottom: calc(var(--input-padding-y) / 3);
}

/* - FIREFOX & CHROME
  Input Box on Focus
*/
.form-label-group input:focus {
  padding-top: 16px;
}

/* - FIREFOX & CHROME
  Input Box Label with typing
*/
.form-label-group input:not(:placeholder-shown) ~ label {
  padding-top: calc(var(--input-padding-y) / 3);
  padding-bottom: calc(var(--input-padding-y) / 3);
  font-size: 9px;
  color: #777;
}

/* - INTERNET EXPLORER
  Input Box Label with typing
*/
input:not(::placeholder) ~ label {
  @media screen and (min-width:0\0) {
    margin-top: 2px !important;
    margin-left: 4px !important;
    font-size: 9px;
    color: #777;
  }
}

/* - FIREFOX & CHROME
  Input Box Label on Focus
*/
.form-label-group input:focus ~ label {
  padding-top: calc(var(--input-padding-y) / 3);
  padding-bottom: calc(var(--input-padding-y) / 3);
  font-size: 9px;
  color: blue;
}

/* - INTERNET EXPLORER
  Input Box Label on Focus
*/
.form-label-group input:focus ~ label {
  @media screen and (min-width:0\0) {
    margin-top: 2px !important;
    margin-left: 4px !important;
  }
}

/* - FIREFOX
  TextArea Box
*/
.form-label-group textarea:not(:placeholder-shown) {
  padding-top: calc(var(--input-padding-y) + var(--input-padding-y) * (2 / 3));
  padding-bottom: calc(var(--input-padding-y) / 3);
}

/* - FIREFOX & CHROME
  TextArea Box on Focus
*/
.form-label-group textarea:focus {
  padding-top: 16px;
}

/* - FIREFOX & CHROME
  TextArea Box Label with typing
*/
.form-label-group textarea:not(:placeholder-shown) ~ label {
  padding-top: calc(var(--input-padding-y) / 3);
  padding-bottom: calc(var(--input-padding-y) / 3);
  font-size: 9px;
  color: #777;
}

/* - INTERNET EXPLORER
  TextArea Box Label with typing
*/
textarea:not(::placeholder) {
  @media screen and (min-width:0\0) {
    padding-top: 12px !important;
    padding-left: 14px !important;
  }
}

/* - INTERNET EXPLORER
  TextArea Box Label with typing
*/
textarea:not(::placeholder) ~ label {
  @media screen and (min-width:0\0) {
    margin-top: 2px !important;
    margin-left: 4px !important;
    font-size: 9px;
    color: #777;
  }
}

/* - FIREFOX & CHROME
  TextArea Box Label on Focus
*/
.form-label-group textarea:focus ~ label {
  padding-top: calc(var(--input-padding-y) / 3);
  padding-bottom: calc(var(--input-padding-y) / 3);
  font-size: 9px;
  color: blue;
}

/* - INTERNET EXPLORER
  TextArea Box Label on Focus
*/
.form-label-group textarea:focus ~ label {
  @media screen and (min-width:0\0) {
    margin-top: 2px !important;
    margin-left: 4px !important;
  }
}

.form-label-group select:not(:invalid) {
  padding-top: calc(var(--input-padding-y) + var(--input-padding-y) * (2 / 3));
  padding-bottom: calc(var(--input-padding-y) / 3);
}

/* - INTERNET EXPLORER
  TextArea Box Label with typing
*/
.form-label-group select:not(:invalid) {
  @media screen and (min-width:0\0) {
    padding-top: 12px !important;
    padding-left: 14px !important;
  }
}

.form-label-group select:not(:invalid) ~ label {
  padding-top: calc(var(--input-padding-y) / 3);
  padding-bottom: calc(var(--input-padding-y) / 3);
  font-size: 9px;
  color: #777;
  content: ''
}

/* - INTERNET EXPLORER
  Select Dropdown Label with option selected
*/
.form-label-group select:not(:invalid) ~ label {
  @media screen and (min-width:0\0) {
    margin-top: 2px !important;
    margin-left: 4px !important;
    font-size: 9px;
    color: #777;
  }
}

/* - FIREFOX & CHROME
  Select Dropdown Label on Focus
*/
.form-label-group select:focus ~ label {
  padding-top: calc(var(--input-padding-y) / 3);
  padding-bottom: calc(var(--input-padding-y) / 3);
  font-size: 9px;
  color: blue;
}

/* - INTERNET EXPLORER
  Select Dropdown Label on Focus
*/
.form-label-group select:focus ~ label {
  @media screen and (min-width:0\0) {
    margin-top: 2px !important;
    margin-left: 4px !important;
  }
}

.form-label-group select:invalid {
  margin-bottom: 0;
  @media screen and (-webkit-min-device-pixel-ratio:0) {
    font-size: 14px;
  }
  line-height: 1.5;
  transition: all 0.1s ease-in-out;
  @media screen and (min-width:0\0) {
    color: #000;
  }
  @media screen and (-webkit-min-device-pixel-ratio:0) {
    color: #000;
  }
}

.form-label-group select:invalid::-ms-value {
  @media screen and (min-width:0\0) {
    color: #fff;
  }
}

.form-label-group select:not(:invalid) {
  color: #000;
}

/* - INTERNET EXPLORER
  Fix input box's native handeling of text
*/
input {
  @media screen and (min-width:0\0) {
    padding-top: 18px !important;
    padding-top: 12px !important;
  }
}

#nprogress .bar {
  background: $color-link-text;
}
</style>
