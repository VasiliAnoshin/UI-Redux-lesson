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
