---
title: "Promises in JavaScript"
seoTitle: "Promises in JavaScript: A Beginner's Guide to Asynchronous Programming"
seoDescription: "Discover the magic of JavaScript promises as a beginner. This comprehensive guide walks you through the fundamentals of Promises in JavaScript"
datePublished: Fri Sep 01 2023 13:23:51 GMT+0000 (Coordinated Universal Time)
cuid: clm0mlwu800000ajgeqkobeo2
slug: promises-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693574397574/f713e701-4514-4268-99f5-45b00ed56449.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1693574422651/959513db-8022-4428-899a-2cf872f8c2d4.png
tags: javascript, javascript-interview-question, javascript-promises

---

### **What is a promise?**

A promise is an object representing the eventual completion of an asynchronous operation. Promises are used to handle asynchronous operations in JavaScript more easily. Before promises, we used callbacks to handle async JavaScript but it led to issues:

1. **Callback Hell**: Callback hell, also known as "Pyramid of Doom," is a term used to describe a situation in asynchronous JavaScript programming where you have a deeply nested structure of callbacks.
    
2. **Inversion of Control:** Inversion of Control, control over the execution flow of a program is transferred from the main application to functions that are passed as callbacks.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693575440007/6663ee54-27a4-4b51-bdfd-273d6e2e4219.png align="center")

A promise is in one of these states:

* ***pending***: initial state, neither fulfilled nor rejected.
    
* ***fulfilled***: meaning that the operation was completed successfully.
    
* ***rejected***: meaning that the operation failed.
    

### Creating a Promise

```javascript
const myPromise = new Promise((resolve, reject) => {
	setTimeout(() => {
		const data = { msg: 'Data fetched' };
		resolve(data);
	}, 2000);
});

myPromise.then((data) => {
	console.log(data.msg);
});
```

**Explaining the code:**

1. We create a Promise (`myPromise`) that represents an operation that will take some time to complete.
    
2. Inside the Promise, we use `setTimeout` to simulate a delay of 2 seconds (2000 milliseconds).
    
3. After the 2-second delay, we create a data object with a message (`'Data fetched'`) and use `resolve` to say that the operation is successful, passing the data.
    
4. We then use `.then()` on `myPromise` to specify what should happen when the operation is done. In this case, we log the message from the data object to the console.
    

### Promises methods

1. **Promise**: It represents the completion/fulfillment of a single asynchronous operation. It resolves when the asynchronous operation is fulfilled successfully and rejected when the asynchronous operation rejects.
    
2. **Promise.all**: It waits for all the input Promises to be fulfilled or one to be rejected. It resolves when all the input Promises get resolved and rejects when any of the input Promises get rejected.
    
3. **Promise.race**: It resolves or rejects as soon as one Promises settles. It resolves when the first input Promise is fulfilled and similarly for reject.
    
4. **Promise.allSettled**: It waits for all input Promises to get settled. It resolves when all the input Promises have settled and It never rejects and handles all Promise states.
    

### Chaining Promises

Chaining in promises is a powerful feature that allows clean and orderly execution of sequences of asynchronous operations. With Wise chaining, you can ensure that one asynchronous operation completes before the next operation begins, allowing you to handle errors more efficiently.

1. **Promise Callback**: When you issue a promise from the .then() call, the next .then() call in the chain has a value that runs on. This allows you to create a series of asynchronous tasks.
    
2. **Error handling**: You can use .catch() at the end of the chain to handle errors that occur at any point in the chain. Thus, there is a centralized error-handling mechanism
    

```javascript
function fetchUserData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      const userData = { username: 'john_doe', id: 123 };
      console.log('Step 1: User data fetched');
      resolve(userData);
    }, 1000);
  });
}

function fetchUserPosts(userData) {
  return new Promise((resolve) => {
    setTimeout(() => {
      const userPosts = ['Post 1', 'Post 2', 'Post 3'];
      console.log('Step 2: User posts fetched');
      resolve(userPosts);
    }, 1000);
  });
}

function displayPosts(userPosts) {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log('Step 3: Displaying user posts');
      userPosts.forEach((post, index) => {
        console.log(`Post ${index + 1}: ${post}`);
      });
      resolve();
    }, 1000);
  });
}

// Chain the Promises together
fetchUserData()
  .then(fetchUserPosts)
  .then(displayPosts)
  .then(() => {
    console.log('All steps completed');
  })
  .catch((error) => {
    console.error('Error:', error);
  });
```

**Thank you for reading 😊**

**I hope you enjoyed it, see you next time** 👋