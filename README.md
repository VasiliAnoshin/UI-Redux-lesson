# To-Do Goals Project

This repo is a code-along project for the React & Redux Course of the [React Nanodegree program](https://www.udacity.com/course/react-nanodegree--nd019).

## Project Setup

1. Clone the Project - git clone https://github.com/udacity/reactnd-redux-todos-goals.git
2. Go into the directory where the project now lives - `cd reactnd-redux-todos-goals`
3. Install the dependencies - `npm install`
4. Start the app - `npm start`

<h4>Lesson Challenge #1 </h4>
Articles: https://blog.pusher.com/the-what-and-why-of-redux/ and https://css-tricks.com/learning-react-redux/. 

1) What are the advantages of using Redux?</br>
2) Describe the 3 principles Redux follows.
<h4>Single Source of Truth:</h4> I’ve mentioned the need for this. Redux has what it calls the store. A store is an object that contains your whole application state. The different pieces of state are stored in an object tree. This makes it easier to implement Undo/Redo. For example, we can store and track the items in a shopping cart and also the currently selected product with Redux and this can be modeled in the store as follows:
<pre>
<code>
<pre class=" language-javascript"><code class=" language-javascript">    <span class="token punctuation">{</span>
        <span class="token string">"cartItem"</span> <span class="token punctuation">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{</span>
                <span class="token string">"productName"</span> <span class="token punctuation">:</span> <span class="token string">"laser"</span><span class="token punctuation">,</span>
                <span class="token string">"quantity"</span> <span class="token punctuation">:</span> <span class="token number">2</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span>
                <span class="token string">"productName"</span> <span class="token punctuation">:</span> <span class="token string">"shirt"</span><span class="token punctuation">,</span>
                <span class="token string">"quantity"</span> <span class="token punctuation">:</span> <span class="token number">2</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">]</span><span class="token punctuation">,</span>
        <span class="token string">"selectedProduct"</span> <span class="token punctuation">:</span> <span class="token punctuation">{</span>
            <span class="token string">"productName"</span> <span class="token punctuation">:</span> <span class="token string">"Smiggle"</span><span class="token punctuation">,</span>
            <span class="token string">"description"</span> <span class="token punctuation">:</span> <span class="token string">"Lorem ipsum ... "</span><span class="token punctuation">,</span>
            <span class="token string">"price"</span> <span class="token punctuation">:</span> <span class="token string">"$30.04"</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
</code></pre>
</code>
</pre>
<h5>State is read-only:</h5> The state cannot be changed directly by the view or any other process (maybe as a result of network callback or some other event). In order to change the state, you must express your intent by emitting an action. An action is a plain object describing your intent, and it contains a type property and some other data. Actions can be logged and later replayed which makes it good for debugging and testing purpose. Following our shopping cart example, we can fire an action as follows:
<pre>
<code class=" language-javascript">    store<span class="token punctuation">.</span><span class="token function">dispatch</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
      type<span class="token punctuation">:</span> <span class="token string">'New_CART_ITEM'</span><span class="token punctuation">,</span>
      payload<span class="token punctuation">:</span> <span class="token punctuation">{</span>
                   <span class="token string">"productName"</span> <span class="token punctuation">:</span> <span class="token string">"Samsung S4"</span><span class="token punctuation">,</span>
                   <span class="token string">"quantity"</span> <span class="token punctuation">:</span> <span class="token number">2</span>
                <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">)</span>
    <span class="token function">dispatch</span><span class="token punctuation">(</span>action<span class="token punctuation">)</span> emits the action<span class="token punctuation">,</span> and is the only way to trigger a state change<span class="token punctuation">.</span> To retrieve the state tree<span class="token punctuation">,</span> you call store<span class="token punctuation">.</span><span class="token function">getState</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>
</code>
</pre>
<h5>Reducer: </h5> The reducers are responsible for figuring out what state changes need to happen and then transforming it to reflect the new changes. Reducer is a pure function that takes in the previous (the current state about to be changed) and an action, determine how to update the state based on the action type, transforms it and returns the next state (the updated state). Continuing with our shopping cart example, let us say we want to add a new item to the cart. We dispatch an action of type NEW_CART_ITEM and, within the reducer, we determine how to process this new change request by reading through the action type and acting accordingly. For the shopping cart, it’ll be adding a new product to the cart:
<pre>
<code class=" language-javascript">    <span class="token keyword">function</span> <span class="token function">shoppingCart</span><span class="token punctuation">(</span>state <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">,</span> action<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      <span class="token keyword">switch</span> <span class="token punctuation">(</span>action<span class="token punctuation">.</span>type<span class="token punctuation">)</span> <span class="token punctuation">{</span>
        <span class="token keyword">case</span> <span class="token string">'New_CART_ITEM'</span><span class="token punctuation">:</span>
          <span class="token keyword">return</span> <span class="token punctuation">[</span><span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>state<span class="token punctuation">,</span> action<span class="token punctuation">.</span>payload<span class="token punctuation">]</span>
        <span class="token keyword">default</span><span class="token punctuation">:</span>
          <span class="token keyword">return</span> state
      <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
</code>
</pre>
What we did was to return a new state which is a collection of the old cart items, in addition to the new one from the action. Rather than mutate the previous state, you should return a new state object, and this really helps with time travel debugging. There are things you should never do inside a reducer, and they are:
<ul>
<li>Mutate its arguments.</li>
<li>Perform side effects like API calls and routing transitions.</li>
<li>Call non-pure functions.</li>
</ul>
