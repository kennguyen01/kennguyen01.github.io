---
title: Make a Chatbot with IBM Watson Part 1
date: 2018-10-08
categories: technology
---

![Chatbot](images/chatbot.jpg)

Here is the link to part 2: [Part 2](/technology/make-a-chatbot-with-ibm-watson-part-2.html)

I recently had an opportunity to play around with [Watson Assistant](https://www.ibm.com/cloud/watson-assistant/) on IBM Cloud. It was pretty fun to implement a simple chatbot from the user’s perspective. I didn’t really need to code anything to get the chatbot up and running. That would be something I want to do in the future. Once I get my feet wet with Machine Learning and Natural Language Processing libraries available on Python.

<!--more-->

## What Do I Use a Chatbot For?

Big companies such as Starbucks, Spotify, and Mastercard have already made extensive use of chatbots. But I can definitely see the appeal of chatbots for small businesses. If I’m the owner of a small business, having a chatbot on my website would save me time and money. Customers would be able to get the information they want quickly without having to navigate through different pages of the website. A well-designed chatbot can also helps customers to make purchase decisions with suggestions.

I want to use this post to provide a quick guide on how to make a simple chatbot with Watson Assistant. Of course there are many chatbot providers out there for you to use. I’m just using IBM because developing a chatbot on its platform is relatively simple. You would have to sign up for a free IBM account so here is the link: [IBM Cloud Registration](https://console.bluemix.net/registration/). It’s a free account and you don’t need to give them your credit card information or anything like that. Once you confirm the registration from your email and log in, let’s get started.

## Making an Assistant

You will be in the dashboard after you logged into IBM Cloud. On the top right corner you will see a search bar. Enter “watson assistant” and a dropdown will appear. Select the option to search in the Catalogs.

![Watson search](/images/watson-search.jpg)

That will open a new tab with a box that says **Watson Assistant (formerly Conversation)**. Clicking on it will open the service window for Watson Assistant. Here you can read the description of the service along with setup options you can choose for your service.

![Service description](/images/service-description.jpg)

On the right hand side, you can assign a name for the service. I name my **Video Game Store Chatbot** because that’s what I will be making. For the region/location to deploy in. Choose the location that’s closest to where you are. I live in the East Coast so that’s what I chose. The other options can be left as default.

Now if you scroll down, you will see the **Pricing Plans** for the service. The **Lite Plan** should be the default since we’re using a free account.

![Watson Pricing Plans](/images/watson-pricing-plans.jpg)

The 10,000 API Calls are the limit of how many queries your service can receive each month. Generally each customer question is considered one API Call. Workspaces are just how many chatbots we can build, up to five for free account. I will talk about Intents and Entities as we progress further. Click on **Create** at the bottom to make our Watson Assistant Service.

## Creating Our Workspace

You will then be taken to the Service Page. Click on **Launch Tool** to open the Watson Assistant Introduction. On the top left corner, there’s the option for **Workspaces**. On that page, we can now create our first chatbot.

![Watson workspaces](/images/watson-workspaces.jpg)

When you click on **Create**, you can give your chatbot a name and a description of what it does. I’m just going to go with Bob. On the next screen, we have a few menus to choose from. The first three: Intents, Entities, and Dialog are empty. The last menu, Content Catalog is a list of pre-trained chatbots if you just want to get started right away.

![Watson build](/images/watson-build.jpg)

Intent is what a user wants to do, such as buying a video game or asking about store hours. Entity is the detail of the conversation that lets you tailor the conversation to that user. A user who wants to buy a role-playing game should get different results than one who wants to buy a shooter game. Finally, imagine dialog as a conversation tree where each question and answer by the user will lead to different branches of the tree. Let’s take a look at intents.

## General intents

From here on out, I’m going to use our video game store as the reference. When a user visits our website, he could be looking for a new game, checking out the deals, or trying to find the store location. The intent is the goal of the user. Before we get started on more in-depth intents, let’s create the intent **#greetings** for when the user says hi.

![Intent greetings](/images/intent-greetings.jpg)

Intents are prefixed with the **#** symbol. You type in the name for the intent, a short description, and any examples of greetings you can think of. After you’ve created the first intent, you can click on the **Try It** button in the top right corner. This will open a chat panel for you to test out the chatbot. You will have to wait for a little bit for Watson to train on the new intent. Then you can test a few simple greetings.

![Chatbot try it](/images/chatbot-try-it.jpg)

Notice how the phrase, “How you doing?” is marked as Irrelevant by Watson. You can change that by clicking on it and change the intent to greetings. Watson will then add the phrase to our **#greetings** intent. Using the same concept, you can add other intents such as **#thanks** and **#goodbyes** to our intents. Remember to test out your new intents and let Watson train on those.

![General intents](/images/general-intents.jpg)

## Specific intents

With the general chit chat out of the way, let’s move on to the intents specific to our business. Some of those intents are **#store-hours**, **#location**, and **#games-offered**. You create them the same way you did with previous intents. But with these intents, you would want to think about how the customers are likely to ask our chatbot. Some common questions regarding store hours:
- ur store open on holidays?
- Are you open on the weekend?
- u open late?
- opening time

Remember that the users will not always use correct grammar and vocabulary to ask our chatbot. You would want to use different examples that are not grammatically correct but convey the intent anyway. This will help train Watson. Right now we’re just training our chatbot to correctly recognize the intents. If you test out different examples in the chat panel, the chatbot will not respond back but it will display the most likely intent of the user. By testing out the chatbot with examples, you can help it narrow down the possible intent based on what the user entered.

![Chatbot intents](/images/chatbot-intents.jpg)

Play around with the chatbot until you are satisfied with how it handles the intents of your inputs. In the next post I will discuss entities and dialog flow for our chatbot.
