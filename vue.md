# Vue Cheatsheet

# Table of Contents
- [Expressions](#expressions)
- [Directives](#directives)
- [Directives (NPM)](<#directives(NPM)>)
- [Special attributes](#special-attributes)
- [Interpolation](#interpolation)
- [Refs](#refs)
- [Component](#component)
- [Async component](#async-component)  
- [Props](#props)
- [Props validation](#props-validation)
- [Slot](#slot)
- [Router](#router)
- [Instance options](#instance-options)
- [Vue router (router options)](#vue-router-options)
- [Vuex (store & module options)](#vuex-store-&-module-options)
- [Events](#events)
- [Custom events](#custom-events)
- [Authentication](#authentication)
- [Auto login/logout](#auto-login/logout)
- [Composition API](#composition-api)
- [Utils](#Utils)
  - [Use "this" into inner function](#Use-this-into-inner-function)
  - [Reactive input vs set input](#Reactive-input-vs-set-input)

- [PWA](#PWA)
- [Node-Sass vs Dart-Sass](#Node-Sass-or-Dart-Sass)





- [Libraries You Should Know](#libraries-you-should-know)
- [Tips](#tips)
  - [Nested objects are NOT reactive (by default)](#1-nested-objects-are-not-reactive-by-default)
  - [Learn and use Vuex from the start](#2-learn-and-use-vuex-from-the-start)
  - [When in doubt, re-render](#3-when-in-doubt-re-render)
  - [Learn the difference between props and data](#4-learn-the-difference-between-props-and-data)
  - [Have a plan for loading elements](#5-have-a-plan-for-loading-elements)
  - [Make common filters global](#6-make-common-filters-global)

## Expressions

```vue
<template>
  <div id="app">
    <p>I have a {{ product }}</p>
    <p>{{ product + "s" }}</p>
    <p>{{ isWorking ? "YES" : "NO" }}</p>
    <p>{{ product.getExpiryDate() }}</p>
  </div>
</template>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Directives

#### List of directives

- [v-text](#v-text) (uses the property as the text value of the element)
- [v-html](#v-html) (uses the property as the text value of the element, interpreting HTML)
- [v-if](#v-if) (element inserted/removed based on truthiness)
- [v-show](#v-show) (similar to v-if, but adds the element to the DOM even if falsy. Just sets it to display none)
- [v-for](#v-for) (iterates over an array or iterable object)
- [v-on](#v-on) (listen to DOM events)
- [v-bind](#v-bind) (reactively update an HTML attribute)
- [v-model](#v-model) (sets a two-way binding for form inputs. Updates the model when the user changes the form field value)
- [v-once](#v-once) (render the element and component once only)
- [v-cloak](#v-cloak) (used to hide an element while vue is mounting)

#### v-text

```html
<span v-text="msg"></span>
<!-- same as -->
<span>{{msg}}</span>
```

#### v-html

```html
<div v-html="html"></div>

<script>
  new Vue({
    el: "#widget2",
    data: {
      html: "<b>I am Widget2</b> - Managed by VueJS",
    },
  });
</script>
```

#### v-if

```html
<p v-if="inStock">{{ product }}</p>
<p v-else-if="onSale">...</p>
<p v-else>...</p>
```

#### v-show

```html
<p v-show="showProductDetails">...</p>
```

#### v-for

```html
<li v-for="item in items" :key="item.id">{{ item }}</li>
```

```html
<li v-for="(item, index) in items">{{ item }} - {{ index }}</li>
<!-- array -->
<li v-for="(value, key, index) in object">
  {{ value }} - {{ key }} - {{ index }}
</li>
<!-- object -->
```

```html
<!-- nested -->
<table>
  <template v-for="u in users">
    <tr v-for="t in u.transfers">
      >
      <td>{{ t.amount }}</td>
      <td>{{ t.asset }}</td>
      <td>{{ t.timestamp }}</td>
      >
    </tr>
  </template>
</table>
```

```html
<!-- passing value as a props -->
<cart-product v-for="item in products" :product="item" :key="item.id">
</cart-product>
```

```html
<!-- passing value as a props -->
<li v-for="id in users" :key="id" :set="item = getUserData(id)">
  <img :src="item.avatar" />
  {{ item.name }} {{ item.homepage }}
</li>
```

#### v-on

```html
<!-- method handler -->
<button v-on:click="doThis"></button>
<button @click="doThis"></button>
```

```html
<!-- inline statement -->
<button v-on:click="doThat('hello', $event)"></button>
```

```html
<!-- object syntax -->
<button v-on="{ mousedown: doThis, mouseup: doThat }"></button>
```

```html
<!-- called only if the condition amount > 0 -->
<button @click="amount > 0 && sendMoney()">Send money</button>
```

```html
<!-- pass arguments -->
<my-component @my-event="handleThis"></my-component>
<my-component @my-event="handleThis(123)"></my-component>
<my-component @my-event="handleThis(123, $event)"></my-component>
```

```html
<!-- the submit event will no longer reload the page -->
<form v-on:submit.prevent="onSubmit"></form>
```

```html
<!-- no propagation to up -->
<a v-on:click.stop="doThis"></a>
```

```html
<!-- capture event (before) up when is triggered down (after) -->
<div v-on:click.capture="doThis">...</div>
```

```html
<!-- only trigger handler if event.target is the element itself, not from a child element -->
<div v-on:click.self="doThat">...</div>
```

```html
<!-- the click event will be triggered at most once -->
<a v-on:click.once="doThis"></a>
```

```html
<!-- the scroll event's default behavior (scrolling) will happen  immediately -->
<div v-on:scroll.passive="onScroll">...</div>
```

```html
<!-- modifiers can be chained -->
<a v-on:click.stop.prevent="doThat"></a>
```

#### v-bind

```html
<a v-bind:href="url">...</a>
```

```html
<!-- shorthand -->
<a :href="url">...</a>
```

```html
<!-- binding an object of attributes -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>
```

```html
<!-- with inline string concatenation -->
<img :src="'/path/to/images/' + fileName" />
```

```html
<!-- true or false will add or remove attribute -->
<button :disabled="isButtonDisabled">...</button>
```

```html
<!-- props -->
<my-component :prop="someThing"></my-component>
<child-component v-bind="$props"></child-component>
```

```html
<!-- class binding -->
<div :class="{ active: isActive }">...</div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { active: isActive, classB: isB, classC: isC }]"></div>
```

```html
<!-- style binding -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>
<div :style="{ color: activeColor }">...</div>
```

```html
<!-- dynamically change componen -->
<component :is="currentView"></component>
```

#### v-model

```html
<template>
  <div>
    <input v-model="message" />
    <p>Message is: {{ message }}</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        message: "Hello World",
      };
    },
  };
</script>
```

```html
<!-- v-model limited to -->
<input v-model="firstName" />
<select v-model="selected">
  <option>A</option>
</select>
<textarea v-model="message" placeholder="add multiple lines"></textarea>
```

```html
<!-- modifiers -->
<input v-model.lazy="msg" />
<input v-model.number="age" type="number" />
<input v-model.trim="msg" />
```

```html
<!-- update two data with one input -->
<div id="app">
  <input v-model="fullName" />
  <div>First: {{firstName}}</div>
  <div>Last: {{lastName}}</div>
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      firstName: "",
      lastName: "",
    },
    computed: {
      fullName: {
        get() {
          return `${this.firstName} ${this.lastName}`;
        },
        set(newValue) {
          const m = newValue.match(/(\S*)\s+(.*)/);
          this.firstName = m[1];
          this.lastName = m[2];
        },
      },
    },
  });
</script>
```

```html
<!-- checkbox -->
<!-- return array of anwser -->
<input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
<input type="checkbox" id="john" value="John" v-model="checkedNames" />
<input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
<span>Checked names: {{ checkedNames }}</span>
```

```html
<!-- radio -->
<!-- return one element -->
<input type="radio" id="one" value="One" v-model="picked" />
<input type="radio" id="two" value="Two" v-model="picked" />
<input type="radio" id="three" value="Three" v-model="picked" />
<span>Picked: {{ picked }}</span>
```

```html
<!-- select -->
<select v-model="selected">
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<span>Selected: {{ selected }}</span>

<script>
  new Vue({
    el: "...",
    data: {
      selected: "",
    },
  });
</script>
```

```html
<!-- multiple select -->
<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
<br />
<span>Selected: {{ selected }}</span>
```

#### v-once

```html
<span v-once>This will never change: {{msg}}</span>
```

#### v-cloak

```vue
<template>
  <div v-cloak>
    {{ message }}
  </div>
</template>

<style>
[v-cloak] {
  display: none;
}
</style>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Directives(NPM)

#### List of directives

- [v-hotkey](#v-hotkey) (allows you to bind one or multiple hotkeys to your components)
- [v-click-outside](#v-click-outside) (catch when a click happens outside a component)
- [other](#https://www.telerik.com/blogs/15-must-have-vue-directives-that-will-significantly-maximize-your-productivity)

#### v-hotkey

```vue
<template>
  <div
    v-show="show"
    v-hotkey="{
      esc: onClose,
      'ctrl+enter': onShow,
    }"
  >
    Press `esc` to close me!
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: true,
    };
  },
  methods: {
    onClose() {
      this.show = false;
    },
    onShow() {
      this.show = true;
    },
  },
};
</script>
```

#### v-click-outside

```vue
<template>
  <div class="hello">
    <div class="ffefd5-box" v-click-outside="ffefd5"></div>
    <div class="c13f10-box" v-click-outside="config"></div>
  </div>
</template>

<script>
export default {
  methods: {
    ffefd5(e) {
      console.log("Clicked outside ffefd5!");
    },
    c13f10(e) {
      console.log("Clicked outside c13f10!");
    },
  },
};
</script>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Special attributes

#### List of Special attributes

- [key](#key) (used as a hint for Vue's virtual DOM algorithm to identify VNodes when diffing the new list of nodes against the old list)
- [ref](#ref) (used to register a reference to an element or a child component)
- [is](#is) (used for dynamic components and to work around limitations of in-DOM templates)

#### key

```html
<ul>
  <li v-for="item in items" :key="item.id">...</li>
</ul>
```

#### ref

```markdown
- cannot access them on the initial render - they don't exist yet
- non-reactive
```

```html
<p ref="p">hello</p>
<!-- vm.$refs.p will be the DOM node -->
<child-component ref="child"></child-component>
<!-- vm.$refs.child will be the child component instance -->
<child-component :ref="(el) => child = el"></child-component>
<!-- When bound dynamically, we can define ref as a callback function, passing the element or component instance explicitly -->
```

#### is

```html
<!-- component changes when currentView changes -->
<component :is="currentView"></component>

<!-- necessary because `<my-row>` would be invalid inside -->
<!-- a `<table>` element and so would be hoisted out      -->
<table>
  <tr is="my-row"></tr>
</table>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Interpolation

```html
<span>Message: {{ msg }}</span>
```

```html
<button @click="toogleDetails">
  {‌{ detailsAreVisible ? 'Hide' : 'Show' }} Details
</button>
```

```html
<!-- Using mustaches: <b> yes </b> -->
<p>Using mustaches: {{ rawHtml }}</p>
<!-- Using mustaches: yes -->
<p>Using mustaches: <span v-html="rawHtml"></span></p>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Refs
- It allows to retrieve values from DOM elements when you need them, instead of all the time </br>

```vue
<template>
  <input type="text" ref="usernameInput" />
  <button @click="setUsername">Set username</button>
</template>

<script>
export default {
  data(){
    return{
      username: ''
    }
  },
  methods: {
    setText(){
      this.username = this.$refs.usernameInput.value;
    }
  }
};
</script>
```



<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Component

- [Import component](#Import-component)
- [Dynamic component](#Dynamic-component)
- [Keep alive dynamic component](#Keep-alive-dynamic-component)
- [Teleport](#Teleport)
- [Async component](#Async-component)

#### Import component

```vue
<template>
  <div>
    <ProductComponent></ProductComponent>
  </div>
</template>

<script>
import ProductComponent from @/components/ProductComponent

export default {
  components: { ProductComponent }
};
</script>
```

#### Dynamic component

```vue
<!-- child: active-goals -->
<template>
  <h2>Active Goals</h2>
</template>
```

```vue
<!-- child: manage-goals -->
<template>
  <h2>Manage Goals</h2>
</template>
```

```vue
<!----------------- OPTIMIZED VERSION ----------------------->
<!-- parent -->
<template>
  <div>
    <button v-if="componentSelected === 'active-goals'">Active</button>
    <button v-if="componentSelected === 'manage-goals'">Manage</button>
    <active-goals @click="setComponentSelected('active-goals')"></active-goals>
    <manage-goals @click="setComponentSelected('manage-goals')"></manage-goals>
  </div>
</template>

<script>
export default {
  data() {
    return {
      componentSelected: "active-goals",
    };
  },
  methods: {
    setComponentSelected(cmp) {
      this.componentSelected = cmp;
    },
  },
};
</script>
```

```vue
<!----------------- OPTIMIZED VERSION ----------------------->
<!-- parent -->
<template>
  <div>
    <button v-if="componentSelected === 'active-goals'">Active</button>
    <button v-if="componentSelected === 'manage-goals'">Manage</button>
    <component :is="componentSelected"></component>
  </div>
</template>

<script>
export default {
  data() {
    return {
      componentSelected: "active-goals",
    };
  },
  methods: {
    setComponentSelected(cmp) {
      this.componentSelected = cmp;
    },
  },
};
</script>
```

#### Keep alive dynamic component

```vue
<!-- parent -->
<template>
  <div>
    <button v-if="componentSelected === 'active-goals'">Active</button>
    <button v-if="componentSelected === 'manage-goals'">Manage</button>
    <keep-alive>
      <component :is="componentSelected"></component>
    </keep-alive>
  </div>
</template>

<script>
export default {
  data() {
    return {
      componentSelected: "active-goals",
    };
  },
  methods: {
    setComponentSelected(cmp) {
      this.componentSelected = cmp;
    },
  },
};
</script>
```

#### Teleport

```vue
<!-- es: <teleport to="body"> </error-alert> -->
<template>
  <div>
    <teleport to="CSS_ID_SELECTOR">
      <error-alert></error-alert>
    </teleport>
  </div>
</template>
```

#### Async component

```javascript
/* -- FOR COMPONENT -- */
import { defineAsyncComponent } from "vue";

// simple usage
const AsyncFoo = defineAsyncComponent(() => import("./Foo.vue"));

// with options
const AsyncFooWithOptions = defineAsyncComponent({
  loader: () => import("./Foo.vue"),
  loadingComponent: LoadingComponent,
  errorComponent: ErrorComponent,
  delay: 200,
  timeout: 3000,
});

app.component("asyncfoo-component", AsyncFoo);
app.component("asyncfoowithoptions-component", AsyncFooWithOptions);
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Props

```html
<blog-post title="My journey with Vue"></blog-post>
```

```html
<!-- Dynamically assign the value of a variable -->
<blog-post :title="post.title"></blog-post>
```

```html
<!-- Dynamically assign the value of a complex expression -->
<blog-post :title="post.title + ' by ' + post.author.name"></blog-post>
```

```html
<!-- Passing a Number -->
<blog-post :likes="42"></blog-post>
```

```html
<!-- Passing a Boolean -->
<blog-post :is-published="false"></blog-post>
```

```html
<!-- Passing a Array -->
<blog-post :comment-ids="[234, 266, 273]"></blog-post>
```

```html
<!-- Passing a Object -->
<blog-post :author="{ name: John, age: 23 }"></blog-post>
```

```vue
<template>
  <!-- are equivalent -->
  <blog-post v-bind="post"></blog-post>
  <blog-post v-bind:id="post.id" v-bind:title="post.title"></blog-post>
</template>

<script>
export default {
  data() {
    return {
      post: { id: 1, title: "My Journey with Vue" },
    };
  },
};
</script>
```

```vue
<template>
  <blog-post :title="post.title"></blog-post>
</template>

<!------------------------------------------>

<template>
  <div>Prova +</div>
</template>

<script>
export default {
  props: ["title"],
};
</script>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Props validation

```javascript
export default {
  props: {
    type: String
    required: true,
    default(){ return 'Default name' },
    validator(value){ return ['success', 'warning', 'danger'].includes(value) }
  },
};
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Slot

- [Using a single slot](#Using-a-single-slot)
- [Named slots (multiple slots)](#Named-slots-(multiple-slots))
- [Default element in slot (if content is not provied)](#Default-element-in-slot-(if-content-is-not-provied))
- [Remove slot dinamically (if content is not provied)](#Remove-slot-dinamically-(if-content-is-not-provied))
- [Scoped slots (pass prop from child slot to parent content of slot)](#Scoped-slots-(pass-prop-from-child-slot-to-parent-content-of-slot))


#### Using a single slot

```html
<!-- child -->
<div class="btn-primary">
  <h1>Test</h1>
  <button>PRESS</button>
  <slot></slot>
</div>

<!-- parent -->
<my-button>
  <template>
    <p>Paragaph 1</p>
    <p>Paragaph 2</p>
    <p>Paragaph 3</p>
  </template>
</my-button>

<!-- how it's renders -->
<div class="btn-primary">
  <h1>Test</h1>
  <button>PRESS</button>
  <p>Paragaph 1</p>
  <p>Paragaph 2</p>
  <p>Paragaph 3</p>
</div>
```

#### Named slots (multiple slots)

```html
<!-- attribute: name -->
<!-- child -->
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <slot>Default content</slot>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

```html
<!-- attribute: slot -->
<!-- parent -->
<app-layout>
  <h1 slot="header">Page title</h1>
  <p>The main content</p>
  <p slot="footer">Contact info</p>
</app-layout>
```

```html
<!-- how it's renders -->
<div class="container">
  <header>
    <h1 slot="header">Page title</h1>
  </header>
  <p slot:default>The main content</p>
  <footer>
    <p slot="footer">Contact info</p>
  </footer>
</div
```

#### Default element in slot (if content is not provied)

```html
<!-- child -->
<div class="container">
  <header>
    <slot>
      <h2>Default tag</h2>
    </slot>
  </header>
</div>
```

```html
<!-- parent -->
<app-layout></app-layout>
```

```html
<!-- how it's renders -->
<div class="container">
  <header>
    <slot>
      <h2>Default tag</h2>
    </slot>
  </header>
</div>
```

#### Remove slot dinamically (if content is not provied)

```vue
<!-- child -->
<template>
  <div class="container">
    <header>
      <slot v-if="slotIsPresent"></slot>
    </header>
  </div>
</template>

<script>
export default {
  data(){
    return{
      slotIsPresent: false,
    }
  }
  mounted(){
    this.slotIsPresent = this.$slots.default;
  }
}
</script>
```

```html
<!-- parent -->
<app-layout></app-layout>
```

```html
<!-- without fix -->
<app-layout>
  <div class="container">
    <header></header>
  </div>
</app-layout>
```

```html
<!-- with fix -->
<app-layout>
  <div class="container"></div>
</app-layout>
```

#### Scoped slots (pass prop from child slot to parent content of slot)

```vue
<!-- child -->
<template>
  <ul>
    <li v-for="(goal, index) in goals" :key="goal">
      <slot :goalId:="index" :goalValue="goal"></slot>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      goals: ["Goal1", "Goal2"],
    };
  },
};
</script>
```

```vue
<!-- parent -->
<template>
  <user-info>
    <template v-slot:default="xxx">
      <h2>Goal number {{ xxx.goalId }} contains value: {{ xxx.goalValue }}</h2>
    </template>
  </user-info>
</template>

<script>
export default {
  data() {
    return {
      goals: ["Goal1", "Goal2"],
    };
  },
};
</script>
```

```html
<!-- if all content goes into one slot -->

<!-- 
<template>
  <user-info>
    <template v-slot:default="xxx">
      <h2>Goal number {{ xxx.goalId }} contains value: {{ xxx.goalValue }}</h2>
    </template>
  </user-info>
</template> 
-->

<template>
  <user-info v-slot:default="xxx">
    <h2>Goal number {{ xxx.goalId }} contains value: {{ xxx.goalValue }}</h2>
  </user-info>
</template>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Router


- [Change url](#Change-url)
- [Dynamic route that catches the next url destintion from the query params](#Dynamic-route-that-catches-the-next-url-destintion-from-the-query-params)
- [Route guard (avoid the url access from the url bar for destination in witch is needed authentication)](#Route-guard-(avoid-the-url-access-from-the-url-bar-for-destination-in-witch-is-needed-authentication))

#### Change url

```javascript
this.$router.replace("/xxx");
```

#### Dynamic route based on the presence of query paramas

```javascript
// http:/www.xxxxxxxxxx.com/yyyy?QUERY_PARAM=zzzzz
const redirectUrl = "/" + this.$router.query.QUERY_PARAM;
const redirectUrl = "/" + (this.$router.query.QUERY_PARAM || "otherPath");
this.$router.replace(redirectUrl);
```

#### Route guard (avoid the url access from the url bar for destination in witch is needed authentication)

```javascript
// import store where is store if we are logged in
import store from "./store/index.js";

// add meta attribute
const router = createRouter({
  history: createWebHistory(),
  routes: [
    { path: "/register", component: CoachReg, meta: { requiresAuth: true } },
    { path: "/auth", component: UserAuth, meta: { requiresUnauth: true } },
  ],
});

// check if authentication is needed and if we are ogeed in
router.beforeEach((to, from, next) => {
  if (to.meta.requiresAuth && !store.getters.isAuthenticated) {
    next("/auth");
  } else if (to.meta.requiresUnauth && store.getters.isAuthenticated) {
    next("/coaches");
  } else {
    next();
  }
});
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Instance options

```javascript
export default {
  components: {}
  props: []
  data(){},
  props: {},
  emits: [],
  methods: {},
  computed: {},
  watch: {},

  beforeCreate: {},
  created: {},
  beforeMount: {},
  mounted: {},
  beforeUpdate: {},
  updated: {},
  beforeDestroy: {}
  destroyed: {},
  actived: {},
  deActived: {},

  errorCaptured(){},

  setup(){}
};
```


<details>
<summary>components</summary>
- Components that can be used in the template

```js
import ProductComponent from "@/components/ProductComponent";
import ReviewComponent from "@/components/ReviewComponent";

export default {
  components: {
    ProductComponent,
    ReviewComponent,
  },
};
```
</details>  


<details>
<summary>props</summary>
- Used to pass data to child component

```javascript
export default {
  props: [
    prop1: {
      type: [String, Number],
      required: true,
      default() {
        return { message: 'hello' }
      },
      validator(value) {
        return ['success', 'warning', 'danger'].includes(value)   // The value must match one of these strings
      }
    },
    prop2: { ... }
  ]
};
```
</details>  


<details>
<summary>data</summary>
- Component state

```javascript
export default {
  data(){
    return { ... }
  }
};
```
</details>  


<details>
<summary>emits</summary>

```javascript
// list of custom event from child component
emits: ['custom-event1', 'custom-event2', ... ]

// custom-event1 must be to have 2 arguments when is called in child component
emits: {
  'custom-event1': (arg1, arg2) => {
      if (arg1 && arg2) {
        return true
      } else {
        console.warn('Invalid submit event payload!')
        return false
      }
    }
  }
}
```
</details>  


<details>
<summary>methods</summary>
- Generic functions </br>
- Used for all function thats must re-evaluated every time (every render of the component) </br>


```javascript
export default {
  methods: {
    functionName($event, arg1, arg2, ...){ ... }
  }
};
```

Uses in template (event binding and data binding)
```vue
<template>
  <button @click="functionName(10, 'text')">Add to Cart</button>
</template>
```

```vue
<template>
  <div> {{ functionName(10, 'text') }}
</template>
```
</details>


<details>
<summary>computed</summary>
- Function that return a value </br>
- Used for all function thats must re-evaluated when a inner data value changes </br>
- Used instead of watch when the function is associated to two or more values (with only one is better use the "watch") </br>

```javascript
export default {
  computed: {
    functionName(){
      // ...
      return ...
    },
    functionName(){
      return (arg1, ...) => `${arg1} a tutti`;
    }
  }
};
```

Uses in template (data binding)
```vue
<template>
  <div>{{ functionName }}</div>
</template>
```
</details>  


<details>
<summary>watch</summary>
- Void function </br>
- Must be the same name of a data </br>
- Used when the function doesn't change a data (so there are a initial controllers on value) </br>
- Used when the function have to do different option depends on the value (so there are a initial controllers on value) </br>
- Used to executes some operations, not directly in template </br>
- It is called automatically when the relative data changing</br>

```javascript
export default {
  watch: {
    functionName(newValue, oldValue){
      if (newValue > 50){
        this.counter = 0;
      }
    }
  }
};
```

Uses in template (none)
```markdown
not use in the template
```


</details>

<details>
<summary>lifecycle hooks</summary>

```javascript
export default {
  beforeCreate: {},
  created: {}, // used to insert data SAVED IN APP that you want display from the first render
  beforeMount: {}, 
  mounted: {}, // used to insert FETCH data that you want display (from first render o subsequent)
  beforeUpdate: {},
  updated: {}, 
  beforeDestroy: {}, 
  destroyed: {}, 
  beforeUnmount: {}, 
  unmounted: {}, 
  activated: {}, // execute when the component is under control of the keep-alive
  deactivated: {}, // execute when the component is under control of the keep-alive and it is deactivated
};
```
</details>

<details>
<summary>other options</summary>

```javascript
export default {
  errorCaptured(err, component, details){ ... }, //execute when an error of child component is triggered (render function, what function, hooks, event handler)
  renderTracked({ key, target, type }){ ... } , // This event tells you what operation tracked the component and the target object and key of that operation.
  renderTriggered({ key, target, type }){ ... }, // This event tells you what operation triggered the re-rendering and the target object and key of that operation
};
```
</details>  


<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Vue router (router options)

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Vuex (store & module options)

#### store options

```javascript
import { createStore } from 'vuex';

import moduleName from './component/moduleName.js'

const store = createStore({
  modules: { moduleName: moduleName, ...},
  state(){ return { ... } },
  getters: { someGetter(state, getters, rootState, rootGetters) { ... }},
  mutations: { someMutation(state, payload) { ... }},
  actions: { someAction(context, payload) { ... }},
});
export default store;
```

#### module options

```javascript
// moduleName.js
import mutations from './mutations.js';
import actions from './actions.js';
import getters from './getters.js';

export default {
  namespaced: true,
  state(){ return { ... } },
  mutations,
  actions,
  getters,
};
```

```javascript
//mutations.js

export default {
  functionOne(){ ... },
  functionTwo(){ ... },
  ...
};
```

#### getters

```javascript
const store = createStore({
  state: {
    todos: [
      { id: 1, text: "...", done: true },
      { id: 2, text: "...", done: false },
    ],
  },
  getters: {
    someGetter(state) { return ..... },
  },
});
```

```javascript
todos(state){ return todos; }

store.getters.doneTodos;        // -> [{ id: 1, text: '...', done: true }, { id: 2, text: '...', done: false }]
```

```javascript
doneTodos(state){ return state.todos.filter(todo => todo.done) }

store.getters.doneTodos;        // -> [{ id: 1, text: '...', done: true }]
```

```javascript
doneTodosCount(state, getters){ return getters.doneTodos.length }

store.getters.doneTodos;        // -> 1
```

```javascript
getTodoById: (state) => (id) => {
  return state.todos.find((todo) => todo.id === id);
};

store.getters.getTodoById(2); // -> { id: 2, text: '...', done: false }
```

```javascript
const store = createStore({
  module: {
    foo: {
      getters: {
        someGetter(state, getters, rootState, rootGetters) {
          getters.someOtherGetter; // -> 'foo/someOtherGetter'
          rootGetters.someOtherGetter; // -> 'someOtherGetter'
          rootGetters["bar/someOtherGetter"]; // -> 'bar/someOtherGetter'
        },
      },
    },
  },
});
```

#### mutations

```javascript
// NO ASYNC CODE HERE
```

```javascript
const store = createStore({
  state: {
    count: 0,
  },
  mutations: {
    increment(state, payload) {
      state.count = state.count + payload;
    },
  },
});
```

```javascript
mutations: {
  increment(state, payload) {
    state.count = state.count + payload
  }
}

store.commit('increment', 10);
```

```javascript
mutations: {
  increment(state, payload) {
    state.count = state.count + payload.amount
  }
}

store.commit('increment', { amount: 10 });
```

```javascript
import { SOME_MUTATION } from './mutation-types'
// mutation-types.js  ---   export const SOME_MUTATION = 'SOME_MUTATION'


const store = createStore({
  state: { ... },
  mutations: {
    [SOME_MUTATION] (state) { // mutate state }
  }
})
```

#### actions

```javascript
// ASYNC CODE HERE
```

```vue
<template>
  <div class="product__actions">
    <button @click="addToCart">Add to Cart</button>
  </div>
</template>

<script>
export default {
  props: ["id"],
  methods: {
    addToCart() {
      this.$store.dispatch("cartModule/addToCart", this.id);
    },
  },
};
</script>
```

```javascript
export default {
  namespaced: true,
  state() {
    return { ... }
  },
  mutations: {
    addProductToCart(state, payload) { ... }
  },
  actions: {
    addToCart(context, payload) { context.commit("addProductToCart", product) }
  }
}
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Events

```html
<!-- Calls addToCart method on component -->
<button v-on:click="addToCart">...</button>
<button @click="addToCart">...</button>
```

```html
<!-- Arguments can be passed -->
<my-component @my-event="handleThis"></my-component>
<my-component @my-event="handleThis(123, '123')"></my-component>
<my-component @my-event="handleThis($event, 123, '123')"></my-component>
```

```html
<!-- Enter -->
<input @keyup.enter="submit" />
<input @keyup.13="submit" />
```

```html
<!-- Ctrl + c + (eventualy other)-->
<input @keyup.ctrl.c="onCopy" />
```

```html
<!-- Ctrl + c -->
<input @keyup.ctrl.c.exact="onCopy" />
```

```html
<!-- Click + ctrl -->
<input @keyup.click.ctrl="onCopy" />
```

```markdown
Key modifiers:
.tab
.delete
.esc
.space
.up
.down
.left
.right
.ctrl
.alt
.shift
.meta
```

```markdown
Mouse modifiers:
.left
.right
.middle
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Custom events

```vue
<template>
  <button @click="changeMsg">Click</button>
</template>

<script>
export default {
  name: ChildComponent,
  data() {
    return {
      message: "New message",
    };
  },
  methods: {
    changeMsg() {
      this.$emit("change-message", this.message);
    },
  },
};
</script>

//-----------------------------------------------------------------

<template>
  <ChildComponent @change-message="updateMessage">{{ msg }}</ChildComponent>
</template>

<script>
export default {
  data() {
    return {
      msg: String,
    };
  },
  methods: {
    updateMessage(newMessageValue) {
      this.msg = newMessageValue;
    },
  },
};
</script>
```

#### custom event validation

```javascript
// list of custom event from child component
emits: ['custum-event1', 'custom-event2', ... ]

// custum-event1 must be to have 2 arguments when is called in child component
emits: {
  'custum-event1': (arg1, arg2) => {
      if (arg1 && arg2) {
        return true
      } else {
        console.warn('Invalid submit event payload!')
        return false
      }
    }
  }
}
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Authentication

- Create UserAuth component
- Handle both login and signin
- Insert data prop (es: email, password, other...)
- <i> --maybe check the input validation directly in the input, with css class-- </i>
- Create "submitForm" where check the input form and call a action (this.$store.dispatch('...', {}))
- Blobal state: where save all dataState used for authentication (es: userId, token, tokenExpiration)
- Action: call the async function to the server and pass the response to the mutation
- Mutation: used to save the parmater get from the async call in the action
- (Firebase doesn't save any information about us, so all the util information must be stored into vuex)
- (For logout in firebase is sufficient to reset the global state)

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Auto login/logout

````vue
// App.vue ```vue
<script>
export default {
  computed: {
    didAutoLogout() {
      return this.$store.getters.didAutoLogout;
    },
  },
  created() {
    this.$store.dispatch("tryLogin");
  },
  watch: {
    didAutoLogout(curValue, oldValue) {
      if (curValue && curValue !== oldValue) {
        this.$router.replace("/coaches");
      }
    },
  },
};
</script>
````

```javascript
// /Auth/action.js
let timer;

export default {
  async login(context, payload) {
    return context.dispatch("auth", {
      ...payload,
      mode: "login",
    });
  },
  async signup(context, payload) {
    return context.dispatch("auth", {
      ...payload,
      mode: "signup",
    });
  },
  async auth(context, payload) {
    const mode = payload.mode;
    let url =
      "https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=AIzaSyBvOcmh_Avvu08bFdUHdmJzA06c6vV4h0E";

    if (mode === "signup") {
      url =
        "https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyBvOcmh_Avvu08bFdUHdmJzA06c6vV4h0E";
    }
    const response = await fetch(url, {
      method: "POST",
      body: JSON.stringify({
        email: payload.email,
        password: payload.password,
        returnSecureToken: true,
      }),
    });

    const responseData = await response.json();

    if (!response.ok) {
      const error = new Error(
        responseData.message || "Failed to authenticate. Check your login data."
      );
      throw error;
    }

    const expiresIn = +responseData.expiresIn * 1000;
    // const expiresIn = 5000;
    const expirationDate = new Date().getTime() + expiresIn;

    localStorage.setItem("token", responseData.idToken);
    localStorage.setItem("userId", responseData.localId);
    localStorage.setItem("tokenExpiration", expirationDate);

    timer = setTimeout(function () {
      context.dispatch("autoLogout");
    }, expiresIn);

    context.commit("setUser", {
      token: responseData.idToken,
      userId: responseData.localId,
    });
  },
  tryLogin(context) {
    const token = localStorage.getItem("token");
    const userId = localStorage.getItem("userId");
    const tokenExpiration = localStorage.getItem("tokenExpiration");

    const expiresIn = +tokenExpiration - new Date().getTime();

    if (expiresIn < 0) {
      return;
    }

    timer = setTimeout(function () {
      context.dispatch("autoLogout");
    }, expiresIn);

    if (token && userId) {
      context.commit("setUser", {
        token: token,
        userId: userId,
      });
    }
  },
  logout(context) {
    localStorage.removeItem("token");
    localStorage.removeItem("userId");
    localStorage.removeItem("tokenExpiration");

    clearTimeout(timer);

    context.commit("setUser", {
      token: null,
      userId: null,
    });
  },
  autoLogout(context) {
    context.dispatch("logout");
    context.commit("setAutoLogout");
  },
};
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Composition API

- [Replace data() with ref()](<#Replace-data()-with-ref()>)
  - [Change ref value](#Change-ref-value)
  - [Pass an object to ref()](<#Pass-an-object-to-ref()>)
  - [Pass an object to reactive()](<#Pass-an-object-to-reactive()>)
  - [Pass an reactive object to toRefs()](<#Pass-an-reactive-object-to-toRefs()>)
- [Replace "methods" with regular function](#Replace-"methods"-with-regular-function)
- [Replace "computed propeties" with the "computed" function](#Replace-"computed-propeties"-with-the-"computed"-function)
- [Working with "watchers"](#Working-with-"watchers")
- [Props component](#Props-component)
- [Emit-component](#Emit-component)
- [Lifecycle hooks](#Lifecycle-hooks)
- [Routing, Params & The Composition API](#Routing,-Params-&-The-Composition-API)
- [useRoute & useRouter](#useRoute-&-useRouter)
- [Vuex Composition API](#Vuex-Composition-API)

```markdown
data + methods è computed + watch = setup
```

```javascript
//attrs: attributes (Non-reactive object)
//slots: slots (Non-reactive object)
//emit: emit Events (Method)
setup(props, { attrs, slots, emit }){}
```

#### Replace data() with ref()

```vue
<!-- OLD  -->
<template>
  <h2>{{ userName }} - {{ age }}</h2>
</template>

<script>
export default {
  data() {
    return {
      userName: "Matteo",
      age: 23,
    };
  },
};
</script>
```

```vue
<!-- NEW  -->
<template>
  <h2>{{ userName }} - {{ age }}</h2>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const userNameConst = ref("Matteo");
    const ageConst = ref("Matteo");

    return {
      userName: userNameConst,
      age: ageConst,
    };
  },
};
</script>
```

#### Change ref value

```vue
<script>
import { ref } from "vue";

export default {
  setup() {
    const userNameConst = ref("Matteo");

    setTimeoue(() => {
      userNameConst.value = "Mat"; // OK
      userNameConst = "Mat"; // ERROR
    }, 2000);

    return {
      userName: userNameConst,
    };
  },
};
</script>
```

#### Pass an object to ref()

```vue
<template>
  <h2>{{ user.name }} - {{ user.age }}</h2>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const user = ref({
      name: "Matteo",
      age: 23,
    });

    setTimeoue(() => {
      user.value.name = "M";
      user.value.age = 32;
    }, 2000);

    return {
      user,
    };
  },
};
</script>
```

#### Pass an object to reactive()

```vue
<template>
  <h2>{{ user.name }} - {{ user.age }}</h2>
</template>

<script>
import { reactive } from "vue";

export default {
  setup() {
    const user = reactive({
      name: "Matteo",
      age: 23,
    });

    // no .value
    setTimeoue(() => {
      user.name = "M";
      user.age = 32;
    }, 2000);

    return {
      user,
    };
  },
};
</script>
```

#### Pass an reactive object to toRefs()

```vue
<template>
  <h2>{{ userName }} - {{ age }}</h2>
</template>

<script>
import { reactive, toRefs } from "vue";

export default {
  setup() {
    const user = reactive({
      name: "Matteo",
      age: 23,
    });

    // no .value
    setTimeoue(() => {
      user.name = "M";
      user.age = 32;
    }, 2000);

    const userRefs = toRefs(user);

    return {
      userName: userRefs.name,
      age: userRefs.age,
    };
  },
};
</script>
```

#### Replace "methods" with regular function

```vue
<template>
  <h2>{{ user.name }} - {{ user.age }}</h2>
  <!-- <button @click="user.age = 32">Click</button> -->
  <button @click="setNewAge">Click</button>
</template>

<script>
import { reactive } from "vue";

export default {
  setup() {
    const user = reactive({
      name: "Matteo",
      age: 23,
    });

    function setNewAge() {
      user.age = 32;
    }

    return {
      user,
      setNewAge,
    };
  },
};
</script>
```

#### Replace "computed propeties" with the "computed" function

```vue
<template>
  <h2>
    name:{{ computedFirstName }}, lastName:{{ computedLastName }}, age:{{ age }}
  </h2>
  <div>
    <input type="text" placeholder="First Name" @input="setFirstName" />
    <input type="text" placeholder="First Name" @input="setLastName" />
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const firstName = ref("");
    const lastName = ref("");
    const age = ref(23);

    // const name = computed(() => {
    //   return firstName.value + " " + lastName.value;
    // });

    function setFirstName(value) {
      firstName.value = event.targe.value;
    }

    function setLastName(value) {
      lastName.value = event.targe.value;
    }

    const computedFirstName = computed(() => {
      return firstName.value;
    });

    const computedLastName = computed(() => {
      return lastName.value;
    });

    return {
      setFirstName,
      setLastName,
      computedFirstName,
      computedLastName,
      age,
    };
  },
};
</script>
```

```vue
<template>
  <h2>name:{{ firstName }}, lastName:{{ lastName }}, age:{{ age }}</h2>
  <div>
    <input type="text" placeholder="First Name" v-model="firstName" />
    <input type="text" placeholder="First Name" v-model="lastName" />
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const firstName = ref("");
    const lastName = ref("");
    const age = ref(23);

    return {
      firstName,
      lastName,
      age,
    };
  },
};
</script>
```

#### Working with "watchers"

```vue
<template>
  <h2>name:{{ firstName }}, lastName:{{ lastName }}, age:{{ age }}</h2>
  <div>
    <input type="text" placeholder="First Name" v-model="firstName" />
    <input type="text" placeholder="First Name" v-model="lastName" />
  </div>
</template>

<script>
import { ref, computed, watch } from "vue";

export default {
  setup() {
    const firstName = ref("");
    const lastName = ref("");
    const age = ref(23);

    // watch(firstName, (newValue, oldValue) => {
    //   console.log(newValue, oldValue);
    // })

    watch([firstName, lastName], (newValue, oldValue) => {
      console.log(newValue, oldValue);
    });

    return {
      firstName,
      lastName,
      age,
    };
  },
};
</script>
```

#### Props component

```vue
<!-- CHILD COMPONENT -->
<template>
  <h2>name:{{ firstName }}, lastName:{{ lastName }}, age:{{ age }}</h2>
</template>

<script>
import { computed } from "vue";

export default {
  props: ["firstName", "lastName", "age"],
  setup(props) {
    const firstName = computed(() => {
      return props.firstName;
    });

    const lastName = computed(() => {
      return props.lastName;
    });

    const age = computed(() => {
      return props.age;
    });

    return {
      firstName,
      lastName,
      age,
    };
  },
};
</script>
```

#### Emit component

```vue
<!-- CHILD COMPONENT -->
<template>
  <h2>Emit</h2>
</template>

<script>
import { computed } from "vue";

export default {
  setup(props, { attrs, slots, emit }) {
    emit("save-data", 2);

    return {
      firstName: firstName,
      lastName: lastName,
      age: age,
    };
  },
};
</script>
```

#### Lifecycle hooks

```markdown
- beforeCrate, create: they run at the same time of setup, so the code that used before in option API now goes in the seutp function
- other hooks: they hae the same but starts with "on" (es: beforeMount -> onBeforeMount), all they have to be imported from vue
```

#### Routing, Params & The Composition API

#### useRoute & useRouter

#### Vuex Composition API

```vue
<!-- CHILD COMPONENT -->
<template>
  <h2>{{ counter }}</h2>
  <button @click="inc">Increment</button>
</template>

<script>
import { useStore } from "vuex";

export default {
  setup() {
    const store = useStore();

    const counter = computed(() => {
      return store.getter.counter;
    });

    function inc() {
      store.dispatch("action-incr");
    }

    return {
      inc,
    };
  },
};
</script>
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Utils
#### Use this into inner function
```javascript
export default {
  watch: {
    functionName(newValue, oldValue){
      if (newValue > 50){
        const that = this;
        setTimeout(function() {
          that.counter = 0;
        }, 2000);
      }
    }
  }
};
```



#### Reactive input vs set input
Reactive input
```vue
<template>
  <input type="text" v-model="message">
  <p>{{ message }}</p>
</template>

<script>
  export default {
    data(){
      message: ''
    }
  };
</script>
```

```vue
<template>
  <input type="text" ref="usernameInput" />
  <button @click="setUsername">Set username</button>
</template>

<script>
export default {
  data(){
    return{
      username: ''
    }
  },
  methods: {
    setText(){
      this.username = this.$refs.usernameInput.value;
    }
  }
};
</script>
```

Set input
```vue
<template>
  <input type="text" @input"saveInput">
  <button @click="setText">Set text</button>
  <p>{{ message }}</p>
</template>

<script>
  export default {
    data(){
      inputValue: '',
      message: ''
    }
    methods: {
      saveInput(event){
        this.inputValue = event.target.value
      },
      setText(){
        this.message = this.inputValue
      }
    }
  };
</script>
```



<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Node-Sass or Dart-Sass
- Ther are two type of Sass preprocessor implementation
- CSS preprocessor: is a program that lets you generate CSS from the preprocessor's own unique syntax. It adds some A CSS preprocessor is a program that lets you generate CSS from the preprocessor's own unique syntax.
- **Dart-Sass**: is the primary implementation of Sass, which means it gets new features before any other implementation. It’s fast, easy to install, and it compiles to pure JavaScript which makes it easy to integrate into modern web development workflows.
- **Node-Sass**: is just a wrapper over LibSass (the C implemented version of Sass).




<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Libraries you should know

**[Vue CLI](https://router.vuejs.org)**

Command line interface for rapid Vue development.

**[Vue Router](https://router.vuejs.org)**

Navigation for a Single-Page Application.

**[Vue DevTools](https://github.com/vuejs/vue-devtools)**

Browser extension for debugging Vue applications.

**[Nuxt.js](https://nuxtjs.org)**

Library for server side rendering, code-splitting, hot-reloading, static generation and more.

# Tips

### 1. Nested objects are NOT reactive (by default)

```vue
<script>
export default {
  data () {
    return {
      someVar: ''
    }
  },
  mounted () {
    this.someVar: {
      level1: {
        level2: {
          level3: 'something old'
        }
      }
    }
  },
  methods : {
    changeSomeVar () {
      this.someVar.level1.level2.level3 = 'something new'
    }
  }
}
</>
```

That method looks like it should work, say you have an input that matches `someVar.level1.level2.level3`, if you ran this method it would not update the model. Instead you need to use `Vue.set` or in a SPC (Single Page Component) you'd just use `this.$set`:

```vue
<script>
export default {
  // ...
  methods: {
    changeSomeVar() {
      this.$set(this.someVar.level1.level2, "level3", "new value here");
    },
  },
};
</>
```

### 2. Learn and use Vuex from the start

This could start a flame war, some Vue fan will tell you to start with an event bus and work your way up, but Vuex is modular enough that you can use it on small and large apps alike. If you're building a SPA there's no chance you'll have fun without Vuex, you're going to implement a lot of the same functionality in your event bus, and making any other developer who works on the project's life a living hell.

A good primer on vuex can be found here: [WTF is Vuex? A Beginner’s Guide To Vue’s Application Data Store](https://vuejsdevelopers.com/2017/05/15/vue-js-what-is-vuex/)

### 3. When in doubt, re-render

Here's a simple use case, say you have an order form that pops up. If for some reason the user closes the order form and reopens it you might find some of the fields won't allow edits, or they have stale data, or if you're triggering the popup via a select box it might not work right. Honestly it's a major headache.

One trick is to re-render your components. The easiest method I've found to do that is whenever a modal or some other component is registered on the DOM pass it a key, or on mount make it generate a random one. A good key could just be to use `Date.now()` or `moment.js` to generate a UTC timestamps and use that.

The key tells Vue that this is a NEW instance, forget about the old one, and let's start over.

### 4. Learn the difference between props and data

Essentially a prop is data that you pass INTO the component from a parent component or on initializing the root component for the first time.

Data is the reactive properties defined on the instance. I find it to be a good practice if you ever think you'll need to update the value or use it re-actively to create a new value on mount that is a duplicate of the prop. So say you have a prop called `colorProp`, you might have a value in data called just `color`, then in your `mounted()` method have `this.color` set to `colorProp`.

### 5. Have a plan for loading elements

You may start out just letting users wait without knowing what's going on but this is going to get dirty fast. Especially when you bring Vuex and multiple data points into the mix. It's best to have a single global **loader** setup that triggers whenever the global **loading** property from Vuex is updated. This way you can always toggle it properly and make sure to un-toggle it.

One caveat is though - be sure you catch all errors - especially when using axios and promises and be sure to end the loading message on errors so users can go back, fix things and resubmit the form.

### 6. Make common filters global

The example below is a bad example on how you should be using filters:

```vue
<template>
  <div>
    <!-- Bad idea -->
    <input type="text" .. /> ${{ moneyVar | money }}
  </div>
</template>

<script>
export default {
  data() {
    moneyVar: 3.5;
  },
  filters: {
    money: function (value) {
      if (!value) {
        return "0.00";
      }
      return "$" + parseFloat(value).toFixed(2);
    },
  },
};
</script>
```

We should make it a global filter:

```vue
<script>
Vue.filter("money", function (value) {
  if (!value) {
    return "0.00";
  }
  return "$" + parseFloat(value).toFixed(2);
});
</script>
```

```

```

```

```

```

```

```

```
