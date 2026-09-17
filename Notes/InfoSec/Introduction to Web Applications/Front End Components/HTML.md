
2025-07-21 15:30

Tags: #web  

## HTML

- **HTML (HyperText Markup Language)** is the fundamental component for creating web pages.

- It *defines the basic structure and content of a webpage* using elements such as titles, forms, and images.

- **Web browsers** parse HTML code to render and display the page to the end-user.


## HTML Structure

- An HTML document is organized in a **tree-like structure**.

- The root element is `<html>`, which contains the `<head>` and `<body>` elements.
	- The `<head>` contains metadata not directly displayed on the page, like the `<title>`, `<style>`, and `<script>` tags.
	- The `<body>` contains all the visible content, such as headings (`<h1>`) and paragraphs (`<p>`).

- Elements are defined by an opening and closing **tag**. Tags can contain attributes like `id` and `class` used by CSS and JavaScript.


## URL Encoding

- Also known as **percent-encoding**, it is used to *encode characters in a URL* that are *outside the standard ASCII* character set.

- This process replaces unsafe characters with a `%` symbol followed by two hexadecimal digits.

- For example, a space character is encoded as `%20` or `+`, and a single quote `'` is encoded as `%27`.

- [Full URL Encoding table](https://www.w3schools.com/tags/ref_urlencode.ASP)


## Document Object Model (DOM)

- **DOM** is a structured, *tree-like representation of a webpage's elements* that allows languages like **JavaScript** to *dynamically access and manipulate* the page's content, style, and structure.

![[Pasted image 20250723120839.png]]

- It has three parts: **Core DOM**, **XML DOM**, and **HTML DOM**.

- Understanding the DOM is critical for locating and manipulating specific page elements, which is a key concept in exploiting front-end vulnerabilities like **Cross-Site Scripting (XSS)**.

## References:

https://academy.hackthebox.com/module/75/section/753