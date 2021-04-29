# Frontend testing 
---


In this article I'm going to try to explain why tests are one of the most important process that we need to considerate at the hour of working on a project. 

## Why we write automated tests? 

***

This is an important question, that maybe we are asked by our clients when we are building an application. 

_Why should I invest my money on writing tests, insted of using that time in working on new features?_

In my opinion, that the most strong asnwer for this question, is **CONFIDENCE**. Thats right, we as developers need to be confident that the code that we are modifing, doesnt broke anything that was already built. Imagine yourself going to the mechanic because the window of your car doesnt work proppely. And then when you receive the fixed window, it turns up that a door is broken. So the first thing that you would do is not bringing the car to that mechanic. So the client looses all type of confidence with us. And that's why we need to be confidence, we need to have a safe net in order not to brake anything that was already working. 

**Documentation**, tests describes how the code should behave. So tests help us understand the business logic without entering on implementation details that may be confuses. 



## What we should test? 🤔

***

So we have this pyramid (taken from the backend) that describes the different types of tests that we could have on our application. 
![Testing pyramids](https://user-images.githubusercontent.com/19891817/116492018-9f298000-a871-11eb-9d4b-765612107e41.png)

This pyramid represents the types of tests that should be included in an automated test suite. Representing, as well, the amount-importance that the type of test should appear. 

| Type | Desciption | Tools
| ---- | ------- | -----
| Static | In charge of catching syntax errors, bad practices and incorrect use of API's. This ones are the most basics ones. | Prettier, Linting, TypeScript, Eslint.
|Unit | This ones describes the business logic behaind the app. They could verify tricky algorthms. They run iosolated. | Jest
| Integration | Give us confidence that all features of your app works correctly together. | React-testing-library, Jest, Enzyme. 
| E2E | This ones verify that whe app works as a whole. It's a transversional tests, that includes frontend suach as backend. | Detox, Cypress|

So this architecture works perfectly with a backend persepctive. But when it comes to frontend architecture maybe we should consider some other things. 

For example. When it comes to **Static** tests, these ones, works perfectly. We can have a TS project, with some fantastic ESlint, and so one, or even have PropTypes in order to avoid having bugs from the beginning. 
But when we are talking about **Unit** tests.

- Are they as effective as they are at the backend? 
- Do we want to tests isoleted components? 

What I'm trying to point out here is that testing isolated component turns up being pointless. I am not saying that Unit test is not important. In deed is very important but we need to be sure **what to tests,**  we dont want to be testing things that doesnt give us any confideence of the correctitud of our code. 
Usually when it comes to componetns, we would want to test a whole Home screen, or in a carousel, when we click on the button it swithces to the next slide. 

So perhaps we need to modify a little bit the pyramid tha we stole from the backend testing suite. 

Let me introduce you to the ... 

### TESTING TROPHY!! 🏆

![Testing pyramids-Page-2](https://user-images.githubusercontent.com/19891817/116492034-a81a5180-a871-11eb-9dbc-f443295e77b9.png)


Here we could notice that **static** testing is still a big part of the testing in the frontend. 
But then, we could see that **Unit** tesitng, although they **EXISTS!** but the are not in a huge amount as they were at the pyramid diagram. 
And then, we have **Integration** test as the winner of the tests 😂. (We will come back to this part later on.)
ANd last but not least. e have **E2E** tests asi an important tests but we all know that they arent going to be as much as the integrations tests. 



## Testing best practices 


***

In this section we are going to go over some importas considerations that we need to have when writing tests. 



### Avoid testing internals

This is a very important concept, that I am going to take a couple of minutes trying to be as clear as possible. 

So lets start defainign what _Avoid testing internals_ actually means. <br>
Someone (I don't know who, but thanks anyway) ones said: 

> "Good tests verify that the external behavior is correct but dont know any implementation details."

So how can we detect that we are testing implementations details? 

**If your test does something that the consumer of your code doesnt then itsl testing implementation details**

For example: Using a private function that we just exposed it just for the tests. 

**If a refactor brakes your tests, then it's testing implementations details**

Making the implementation the same, but changing how its implemented, would brake your tests. And this woould end up not liking writing tests.
>"Every time I make a change to the code, the tests break!"

<br> So testing implementations details would leed us to too posible scenarios: 
1. Test can brake when you refactor your code, but still works in production **False-Negative**
2. Test may not fail, but brakes the application **False-Positive**

<br>

### Tests should be deterministic

> "A non deterministic test is a test that sometimes passes and somentimes doesnt"

This happens for different resosn
 - Timezones 
 - File system 
 - Database
 - Shared states between tests
 - Timeouts

### Avoid unneccesarry expectations and tests 

```js

expect(obj).toBeDefined();
expect(obj).toHaveAProperty('prop1', 'prop2')

```

The first expectation is useless. 





### 4) Not too many 



### 5) Mostly implementation tests 

## Conclusion

