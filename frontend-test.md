
# Thinking frontend testing
---

![7ucwd-440539-Full-Image_GalleryBackground-en-US-1589489689649 _SX1080_](https://user-images.githubusercontent.com/19891817/116832269-a1018500-ab8a-11eb-9f78-aa95422f1a9c.jpg)


In this article I'm going to try to explain why tests are one of the most important process that we need to considerate at the hour of working on a project. 

## Why we write automated tests? 
***

An essential question that maybe we are asked by our clients when we are building an application.

_Why should I invest my money in writing tests instead of using that time in working on new features?_

The best answer to this question is **CONFIDENCE**. That's right, we as developers need to be confident that the code that we are modifying doesn't break anything that it's already working. Imagine yourself going to the mechanic because the window of your car doesn't work correctly. And then when you receive the fixed window, it turns up that a door was broken. So the first thing that you would do is not bringing the car to that mechanic anymore. So the client loses all types of confidence in us. And that's why we need to be confident; we need to have a safety net that protects us from breaking anything that was already working.

Another important reason why we should write automated tests is **DOCUMENTATION**. Tests describe how the code should behave. So tests help us understand the business logic without entering on implementation details that may be confusing.

## What we should test? 🤔
***

The testing pyramid describes the different types of tests that we could have on our application. 

![Testing pyramids](https://user-images.githubusercontent.com/19891817/116492018-9f298000-a871-11eb-9d4b-765612107e41.png)

This pyramid represents the types of tests that should be included in an automated test suite.

| Type | Description | Tools
| ---- | ------- | -----
| Static | In charge of catching syntax errors, bad practices, and incorrect use of APIs. These are the most basics ones. | Prettier, Linting, TypeScript, Eslint.
|Unit | These describe the business logic behind the app. They could verify tricky algorithms. They run isolated. | Jest
| Integration | Give us confidence that all features of your app work correctly together. | React-testing-library, Jest, Enzyme. 
| E2E | These verify that the app works as a whole. It's a transversional test that includes frontend such as backend. | Detox, Cypress|

So this architecture works perfectly with a backend perspective. But when it comes to frontend architecture, maybe we should consider some other things. 

For example; When it comes to **Static** tests, these work perfectly well considering both; backend and frontend. We can have a TS project with some fantastic TSlint, and so on, or even have PropTypes to avoid having bugs from the beginning. 
But when we are talking about **Unit** tests, we can ask ourselves some questions: 

- Are they as effective as they are at the backend? 
- Do we want to tests isolated components? 

What I'm trying to point out here is that the isolated testing component turns up being pointless. I am not saying that Unit tests are't necessary. Indeed, they are significant, but we need to be sure **what to tests**. We don't want to be testing things that don't give us any confidence in the correctitude of our code. 
Usually, when it comes to components, we would want to test a whole Home screen or a Carousel; that when we click on the button, it switches to the next slide. In this case, testing separated the button with the carousel is pointless because I want them working as a unit. 
So should have a different pespective for the pyramid that we stole from the backend testing suite. 

### TESTING TROPHY!! 🏆

![Testing pyramids-Page-2](https://user-images.githubusercontent.com/19891817/116492034-a81a5180-a871-11eb-9dbc-f443295e77b9.png)

Here we notice that **static** testing is still a big part of the frontend testing. 
When it comes to **Unit** testing, they **EXISTS!**; but, not in a massive amount as they were at the pyramid diagram. 
**Integration** test is the winner of the tests 😂. (We will come back to this part later on.)
And last but not least. We have **E2E** tests as necessary tests, but we all know that they aren't going to be as much as the integrations tests. 

## Testing best practices 
***

This section will go over some important considerations that we need to have when writing tests.

### Avoid testing internals

We are going to take a couple of minutes trying to be as straightforward as possible. 

So let us start defining what _Avoid testing internals_ means.
<br>
Someone (I don't know who, but thanks anyway) said: 

> "Good tests verify that the external behavior is correct but don't know any implementation details."

So how can we detect that we are testing implementation details? 

**If your test does something that the consumer of your code doesn't, then it's testing implementation details**

For example: Using a private function that we just exposed just for the tests. 

**If a refactor breaks your tests, then it's testing implementations details**

Making the implementation the same, but changing how it's implemented, would break your tests. In other words, when we do a refactor, the idea is to have the same functionality but with a different implementation. Suppose refactoring brakes tests turn up being a total pain to do a test. And this ends up with the programmers not enjoying writing tests.
>"Every time I make a change to the code, the tests break!"
<br>
So testing implementations details would lead us to two possible scenarios: 

 1. Test can break when you refactor your code but still works in production **False-Negative**
 2. Test may not fail, but breaks the application **False-Positive**
<br>

### Tests should be deterministic

> "A non-deterministic test is a test that sometimes passes and sometimes doesn't."

This happens for different resosn
 - Timezones 
 - File system 
 - Database
 - Shared states between tests
 - Timeouts

### Avoid unnecessary expectations and tests 

```js

expect(obj).toBeDefined();
expect(obj).toHaveAProperty('prop1', 'prop2')

```

The first expectation is useless. 

### 4) Not too many 

There is no need to have a 100% of coverage. Theoretically, it's an excellent idea, but in practice, it doesn't apply that much. 
Well, when you strive for 100% all the time, you find yourself spending time testing things that don't need to be tested. 
So striving for 100% of code coverage depends on many things. Let me try to explain it with a graphic. 

![Testing-not-to-many](https://user-images.githubusercontent.com/19891817/116832062-94c8f800-ab89-11eb-9dc6-b2ec18d7ec1d.png)

This graphic shows us how we are going to face our code coverage. 
If we are a start-up and need to implement many features to get funding, we would like to be more at the left-hand side of the sweet spot. 
Or if we are a company having thousands of users using your system, you would rather be on the right side of the sweet spot.


### 5) Mostly integration tests 

So, for now, we have been talking about why we write tests, good practices, and many other things, but one crucial thing that we didn't talk about is, `what should I test`? 

If we consider two important factors that determine whether we implement tests or don't, we would have to think about `money` and `time`. 

So let's go back a little bit to the trophy. 🏆

![Testing-not-to-many-Page-2](https://user-images.githubusercontent.com/19891817/116832104-d2c61c00-ab89-11eb-9e40-911948001ab1.png)

Considering this, you would tell me, so let's choose only the `Static` ones. It's obvious. They are the cheapest and the fastest. 
And yes, you are right. But we need to consider an important issue here, and it's `The problem that does types of tests, solves`, also known as the `confidence coefficient`. 
In other words, statics tests solve the most straightforward problems, and the end-to-end tests, the most more significant issues. 

![Testing-not-to-many-Page-3](https://user-images.githubusercontent.com/19891817/116832131-ebcecd00-ab89-11eb-99af-e53c5d359404.png)

In a `confidence-coefficient-perspective`, integration tests are the best option. So as the title of this section says, `write mostly integration tests`. 
They are: 
- Cheap 
- Fast 
- And Solves most of the problems


## Conclusion

Do as many tests as you feel confident. The more things from the reality that you mock, the less confidence you will have. It's not a matter of code coverage; it's a matter of confidence. 
Test higher up your tree; instead of testing a specific component, test a hole page with all the components working together. 

