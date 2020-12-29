---
title: Creating Popup Modal
date: 2020-12-28
categories: web
---

For the [library project](https://raisingexceptions.com/top-projects/library/) on The Odin Project, I spent a few hours learning how to make a modal. I did not have to make one, but I had fun learning how to do it. This post is a quick guide on making a popup modal. I pulled this straight from the library project. You can adjust it as needed.

<!--more-->

## HTML

We need a button that opens the modal. We can add an event listener here to trigger the modal.

```html
<button class="open-modal" type="button">Add Book</button>
```

The content is placed inside the modal container. The purposes of the container are to hide the content and provide a fixed position for the modal.

```html
<div class="modal">
  <div class="modal-content">
    <span class="close-modal">&times;</span>

    <fieldset class="book-info">
      <legend>Add New Book</legend>

      <label for="title">Title:</label>
      <input id="title" type="text">

      <label for="author">Author:</label>
      <input id="author" type="text">

      <label for="genre">Genre:</label>
      <input id="genre" type="text">
    </fieldset>

    <button class="add" type="button">Add</button>
    <button class="reset" type="button">Reset</button>
    <button class="cancel" type="button">Cancel</button>
  </div>
</div>
```

I chose to group the text input fields inside the fieldset for organization. If you want to use the modal for popup dialogue, it's unnecessary. The span above the fieldset is the X button for closing the modal.

## CSS

The modal container is hidden with a fixed position. The background can be any color. I used an opacity of 0.3 to highlight the modal when it appears.

```css
.modal {
  display: none;
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.3);
}
```

The modal content is where you can play around with the styling.

```css
.modal-content {
  width: 500px;
  min-height: 200px;
  border-radius: 15px;
  background: #eee;
  margin: 5% auto;
  padding: 1em;
  text-align: center;
}
```

One option for closing the modal is using an X in the top right corner. I added red color and small effects when the user hovers over the X.

```css
.close-modal {
  color: #ff4b5c;
  float: right;
  font-size: 30px;
}
.close-modal:hover,
.close-modal:focus {
  color: red;
  text-decoration: none;
  cursor: pointer;
  transform: scale(1.3);
}
```

The last part is the optional fieldset I had earlier. You can use another div to separate different sections of the content.

```css
.book-info {
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: 2fr 7fr;
  grid-gap: 15px;;
  justify-content: center;
  align-items: center;
  margin: 1em auto;
  font-size: 18px;
}
```

I used a grid layout to make the content center and align evenly. Flexbox also work here.

## JavaScript

Some functions I wrote have the `modal` parameter. I passed in that argument in the IIFE at the end. I wanted to avoid having to query the modal element inside each function. 

```js
/**
 * Open modal when 'Add Book' button clicked.
 * 
 * @param {HTMLElement} modal 
 */
const openModal = (modal) => {
  let open = document.querySelector('.open-modal');
  open.addEventListener('click', () => {
    modal.style.display = 'block';
  });
}
```

There are three ways to close out the modal: X, Cancel, and clicking outside the modal. I wrote a helper function to close the modal for the first two methods.

```js
/**
 * Helper function to close modal.
 * 
 * @param {HTMLElement} modal 
 */
const close = () => {
  let modal = document.querySelector('.modal');
  modal.style.display = 'none';
}

/**
 * Close modal when X clicked.
 */
const closeModal = () => {
  let xSpan = document.querySelector('.close-modal')
  xSpan.addEventListener('click', close);
}

/**
 * Close modal when 'Cancel' button clicked
 */
const cancelModal = () => {
  let cancel = document.querySelector('.cancel')
  cancel.addEventListener('click', close);
}

/**
 * Close modal when user click outside the box
 * 
 * @param {HTMLElement} modal 
 */
const clickOutside = (modal) => {
  window.addEventListener('click', (e) => {
    if (e.target == modal) {
      closeModal();
    }
  });
}
```

A Reset button is often not necessary for a regular modal. I included it here for my own sanity. I tested my own modal many times with different inputs. I needed a Reset button to not having to manually delete previous inputs.

```js
/**
 * Reset modal input fields to default values.
 */
const resetFields = () => {
  let reset = document.querySelector('.reset');
  reset.addEventListener('click', () => {
    document.getElementById('title').value = '';
    document.getElementById('author').value = '';
    document.getElementById('genre').value = '';
  });
}
```

The IIFE at the end of the code runs all the functions above.

```js
(function () {
  let modal = document.querySelector('.modal');
  
  openModal(modal);
  
  closeModal();
  cancelModal();
  clickOutside(modal);
  
  resetFields();
})();
```