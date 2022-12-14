1\. Intro
---------

Welcome; this course will teach you how to write a tutorial from scratch. You have probably benefited a lot from tutorials that others have created, and there are a couple of reasons to create a tutorial yourself:

-   "If you want to master something, teach it" (Richard Feynman). Teaching a subject requires you to learn about it in depth because you need to be able to understand all details and explain it simply and understandably. 
-   You help people in a similar situation as you. You might form new connections with other learners and get your name out to the community.
-   It showcases your skills to potential future collaborators or employers.

This course has tutorials for developers in mind that have a limited amount of experience with creating tutorials. Still, it might also be interesting for a non-technical audience.

The time to complete this course is tough to estimate since it will depend on the subject of the tutorial you want to create and how thoroughly you will follow the instructions. Creating a tutorial might take you anywhere from a couple of days to a couple of months.

In this course we will:
* Choose a topic
* Create a project
* Create the first draft of the tutorial
* Structure the draft
* Finalize the draft

Before we start, let's set up a research document where we can store links from our research, scribble ideas and begin writing drafts. We typically use google docs or markdown files and services like <https://hackmd.io/> to collaborate on them. 

2\. Choose a topic
------------------

The first step of writing a tutorial, and one of the most important ones, is to choose the right topic for your tutorial. Brainstorm and research to find out what technology you want to cover. Think about the project you want to build and what other technologies you wish to use.

### 2.1 Brainstorm technologies

-   Is there new technology, a skill to train, or a buzzword you keep hearing or seeing in job descriptions that you would like to explore in more detail?
-   Is there something you struggled to learn recently because the available documentation and instructions needed to be more sufficient?
-   Is there a technology you mastered and would like to create a great beginner project with?

### 2.2 Research

You want your tutorial to be helpful and read by many people. In that case, you need to find a relevant topic that people want to learn more about, but you also need to choose an angle that has yet to be covered fully.

#### 2.2.1 Research Competition

After you have an idea of what topics you find interesting, is the time to research which and how these topics have already been covered. Google for existing tutorials on the topics, store the links and make notes in your research document. Your competition becomes specifically relevant if they are very popular and have been created recently. 

It's ok if popular tutorials on the topic already exist, but then you should have a different angle for your approach, like combining it with another technology, showing a specific application use case, or targeting a different audience, beginners instead of experts, e.g.

#### 2.2.2 Research Technology 

After you have done your research on the competition, you need to dig a bit deeper into the technology. At this point, you might have already gathered some good tutorials on the topic in your research document. Now add more helpful links to the document that offer good explanations for the technology, like parts of the official documentation.

You should have now developed a basic understanding of the technology you want to cover in your tutorial. Try to do one or two of the most relevant tutorials on the topic that already exist and make notes on explanations that were helpful or how they could have been improved. Keep notes of things you'll want to bring up in your tutorial and save useful links.

### 2.3 Choose an audience

Now that you have an overview of the competition and the technology, you can start thinking about your tutorial and how you want to approach the topic. Based on your findings, for whom should this tutorial be? Do you want to write for beginners or already people familiar with the topic, or even experts and just tackle important new details?

Think about the developer you have in mind as your audience for this tutorial, what skills they need, and what requirements they need to fulfill.

### 2.4 Scope your tutorial

Based on your audience, think about what you want to build in this tutorial, what project the readers will make, and what other technologies you wish to use.

#### 2.4.1 Tutorial project

There are some popular evergreens, especially when creating a tutorial with a front-end like a personal website, a blog, a marketplace, social media platform, or a shop. In web3 contract development, some examples are often used. They are an easy entry for beginners that know these examples from other technologies, like multi-sig, crowdfunding, or auction contracts.

The project you are going to build should have a real-world application with understandable functionality instead of very abstract examples like foo and bar.

It should also be something that people are familiar with, and that could be helpful for them if they want to create their own projects.

#### 2.4.2 Additional technologies

When creating the project, you will most likely need to use additional technology to the one that you focus on explaining. It makes sense to use popular technology that most people are familiar with if you don't have a strong reason against it. E.g., you should use React over another JS framework since it's the most popular one. If you want to write a smart contract for an EVM-based chain, you might consider using Solidity over Vyper.

To compare technologies with each other, it can help to look into how many stars a project has on GitHub and compare that with alternatives.

3\. Create a project
--------------------

In this step, you want to build the project you will write about.

### 3.1 Experiment

You will not build the perfect project on the first try, so give yourself some room to experiment with the code. Your code does not have to be very clean or well-structured yet, now is the time to play around. Just start building what you have in mind as the project to be built in the tutorial. 

Make notes of important parts of your building process and steps that are not working as you had expected. 

You should end up with a project where the code might be unclean and messy but that is working as intended. You should know by now what technologies and dependencies you want to use in the project.

### 3.2 Build the tutorials project

Now it's time to clean up; try to make this tutorial as readable and organized as possible. You can already start commenting on the most important parts of your code at this stage. 

Try to reduce the complexity, especially if you are writing for a beginner or intermediary audience. Still, even for experts, it's helpful that the project is as simple as possible and focuses on the targetted technology.

The project setup should also be as easy as possible without installing obscure dependencies and having to configure the project extensively. Boilerplates like create-react-app, the [Celo Composer](https://github.com/celo-org/celo-composer), or even your own custom boilerplate can be a great way to get the readers started quickly.

Reiterate until you have the final code of your project, with a simple scope, an easy setup, and clean and organized code.

### 3.3 Rebuild from scratch while writing an outline of the tutorial

Now rebuild the project from scratch and create an outline for the tutorial with the most essential instructions while you build it. You can already save important code snippets.

Try to organize the steps necessary for the creation of the project into a logical step-by-step order that represents the progression of the project but also builds up the necessary knowledge on top of each other.

While building and writing the outline, ensure that the code works on all tutorial steps.

4\. Create the first draft of the tutorial
-----------------------------------

In this step, we want to convert the rough outline of the tutorial into a first draft. This version won't have perfect wording yet and won't be structured in the best way. Still, it should contain the core content, with all the steps necessary to create the project explained in the tutorial.

Before you start writing, here are some suggestions for your writing style to keep it as understandable as possible.

### 4.1 Style

#### 4.1.1 Keep it short and simple 

Try to keep the steps that you are explaining as concise as possible. If you feel a step is getting too long, you better split it into two separate steps.

Your sentence should also be as short as possible and your words as small as possible. No need to impress anybody; it is more important to use common words that aren't very abstract and understandable for everybody.

"Short sentences communicate more powerfully than long sentences, and short sentences are usually easier to understand than long sentences" ([Google documentation on technical writing](https://developers.google.com/tech-writing/one/short-sentences)).

Try to stay on topic and focus on content immediately necessary for the tutorial creation. There are many exciting things to cover for a lot of technologies, but it is crucial for the reader that you stay on point and make the content as easy to understand as possible.

#### 4.1.2 Write detailed instructions

An often expressed critique of tutorials is that they are not detailed enough, readers can't follow and get stuck, often abandoning the tutorial. Make sure to give thorough instructions to avoid confusion. If you are explaining abstract concepts, think about concrete examples that illustrate your explanations.

#### 4.1.3 Visualize

Sometimes detailed written instructions are not enough, especially when the user needs to interact with user interfaces. In these cases, screengrabs in the form of images, videos, or GIFs can be very helpful.

Make sure you don't overdo it; a tutorial full of images is hard to get through. A short GIF or a video might be better than 10 images. But a picture that can capture the essence is the best form of visual communication because it doesn't introduce additional friction.

Try to provide captions for visualization, especially for GIFs.

#### 4.1.4 Provide code

Provide code blocks in your tutorial, but keep them focused on the most critical lines. An 80-line code block makes your tutorial hard to read. Break up long blocks of code with explanations in between. Don't create blocks that are longer than the average screen height.

At the end of a step, it is often very helpful to provide a link to the full code of the step, stored on GitHub e.g., provide the full code to download at the end and the beginning of your tutorial.

**4.1.5 Add links to more resources**

If you have explained a concept in a step and think its explanation is insufficient, provide a link to another resource with further explanation.

5\. Structure the draft
------------------------

Now you should have created the first draft of your tutorial and can start to give it a bit more structure and format.

### 5.1 Create a title

While you might change the title later, it's good to start thinking about it and refine it during your process since the title will be the first point of contact with your potential readers.

The title should describe what the tutorial is about. It shouldn't be too long. Try to make it not much longer than 60 characters. It should contain the core technology explained in the tutorial, the type of project that will be built, and maybe the audience and other important parts of the tech stack.

Example:

"How to Build a Full Stack NFT Marketplace on Celo with Next.js"

### 5.2 Write an introduction

The introduction is essential because the reader will decide if they want to do your tutorial here. You should give them the necessary information to help them settle in your favor.

#### 5.2.1 State the learning objective

Write in the initial paragraph what technology they will learn in this tutorial and what they will build. It is also beneficial to provide a demo link or video of what they will develop and the link to the project's repository.

You can also provide some context and let the readers know why learning this technology and building this project is interesting. This is where you want to convince them to start the tutorial and get them excited.

#### 5.2.2 List the tech stack

Next, you should let the reader know which technologies, frameworks, and tools they will use in the tutorial so they can make an informed decision if the tutorial is relevant to them.

Try to give a brief one-sentence explanation of the tech, link to the resources, and, if possible, provide the version number you will use.

#### 5.2.3 Prerequisites and previous knowledge 

It is important to tell your audience what they need to already know before starting the tutorial. Try only to list the essential prerequisites, you can provide a link to a resource to learn them.

#### 5.2.4 Time required

Give your audience an estimate of how much time they will need to do your tutorial. Make sure you are honest and realistic because readers won't be happy if they need a whole afternoon to do your tutorial, and you told them they would only need 30 minutes. It is a good idea to time yourself doing the tutorial and then estimate the time from your experience.

### 5.3 Structure your steps

The steps you have created in the first draft will now form the core building blocks of your tutorial. Now we need to structure them to allow for the best flow and learning experience.

#### 5.3.1 Create Headings
In each step, you should make sure to have a proper heading that describes the topic that is taught in this step. If your tutorial is more extended and has different sections, you can also have section titles between the steps.

Break down your steps into smaller pieces by creating subheadings within your steps. Again, short yet descriptive subheadings will help your audience see what is important in each step and make it easier to understand your content.

#### 5.3.2 Number your steps

You can add numbers to your steps and subheadings to create a visual hierarchy that helps your audience to understand what comes next. Again don't overdo it. If your tutorial is 30 minutes, you don't need 500 steps; 10-15 steps are entirely sufficient.

#### 5.3.3 Add a short description to each step

After the heading and before the explanations, it is a good idea to add a short description that supports the heading and explains what will be taught in this step.

### 5.4 Write an FAQ section

FAQ stands for Frequently Asked Questions, and it can make sense to add this section to your tutorial to answer questions your audience will have. This will also help to reduce your support load as people can have their questions answered directly within the tutorial.

The questions can be taken from the comments in other blogs and tutorials, or you can add your own questions that you have often been asked or are relevant to this tutorial. This can also be a place for some general helpful instructions that didn't fit into any other specific step.

### 5.5 Add a conclusion

The conclusion is the last step of your tutorial. It should be used to summarize and conclude the learned concepts and technology.

You should also link to your project's final source code, add a call to action, and encourage the reader to continue working on the code they've built and add new features.

6\. Finalize the draft
-----------------------

You might have already edited your tutorial based on the suggestions from the previous steps, but now is the time to clean it up and create the final version.

### 6.1 Test your draft thoroughly

Now that you have written and structured your first draft with all the steps, explanations, and solutions, it's time to test if everything works as intended.

This is the most important part of the process; you need to do the tutorial yourself and make sure that everything works as planned! Try to follow the tutorial as if you have no prior experience with it. This will reveal additional steps or solutions you need to add to your tutorial that will enable readers to finish the project without complications.

### 6.2 Revision

After you have done the tutorial and everything works, you should take some time away from it. This is important because you are too close to the content to see any possible errors.

After taking some time away, you should go back and be able to look at your tutorial with a fresh mind and fix problems that you never noticed before.

Never publish the first draft; even if you think it's perfect, it is not. Or, as Hemming put it: "The first draft of anything is shit."

### 6.3 Get feedback

Once you think you are happy with your tutorial, it is time to get feedback. The best approach is to get feedback from your target audience.

You should also reach out to people who know more about the topic and ask them to go through it. The feedback will help you better understand how your tutorial flows and works for people unfamiliar with it.

It can take a lot of work to get people's attention to look at your tutorial, but it is worth it in the end. Ask friends, colleagues, or even strangers on Twitter that are interested in similar content.

### 6.4 Quality assurance

After you have integrated all suggestions and are satisfied with the result, you should check all the code snippets, images, and links to ensure that everything is still up to date and works correctly.

It is a good idea to include in your tutorial when it was last updated.

Ensure your tutorial has proper spelling, grammar, sentence structure, and punctuation. This is one of the first things people notice and will give an early impression of the quality of the content.

Use tools like [Hemingway App](https://www.hemingwayapp.com/) or [Grammarly](https://app.grammarly.com/) for spelling, grammar, and style. You can also ask someone else to read through your tutorial and edit it for typos and syntax errors or hire a professional editor from a service like fiverr.com to proofread your tutorial.

7\. Conclusion
--------------

In this course, you learned how to choose the right topic and project, create your first draft, and structure and finalize it. We hope we could give you some new ideas on how to make a tutorial and a rough guideline that, when followed, helps you create your own great tutorial.

If you are just starting out and are writing your first tutorial, keep in mind that this is a very iterative process and that you will learn and improve with every tutorial you write. Try to get feedback from your readers on how you could enhance the tutorial, which will help you to improve faster.

Here are the next steps that you can take after creating your tutorial.

### 7.1 Next steps

-   Submit your tutorial to the challenge of this course, earn a reward and get feedback from your peers on how to improve upon your tutorial.
-   You can participate in the [Celo Sage program](https://docs.celo.org/community/celo-sage), submit your tutorial there, and be able to earn a bounty of up to 500$.

Thanks a lot for following through on this course. We are excited to get to read what you have created!

8\. FAQ
-------
**What tools can help me to create my tutorial?**
There are many tools and websites that developers can use to create coding tutorials. Here are some that we found helpful.

* AI and LLMs - AI assistants and large language models (LLMs) like [ChatGPT](https://chat.openai.com/) or [GitHub Co-pilot](https://github.com/features/copilot) can help you to create outlines for the tutorial, generate explanations for code, or answer questions.
* Writing-enhancement - Tools like [Grammarly](https://app.grammarly.com/), [ProWritingAid](https://prowritingaid.com/), and [Hemingway Editor](https://hemingwayapp.com/) include grammar checkers, spell checkers, and thesauruses. These tools can help writers improve the accuracy and clarity of their writing.
* Screen-recording - Tools like [Loom](https://), [OBS](https://obsproject.com/), or [Snagit](https://www.techsmith.com/screen-capture.html) allow users to capture their screen, which is particularly helpful when describing interfaces.


**Where should I publish my tutorial?**

There are many different platforms for hosting your content. If you have your own website, you can simply include your tutorial there and have complete control over your content and look. Then you could also have your content as markdown files on Github and render it from there to your website. GitHub also allows you to host your tutorial directly with the help of their Pages feature, which is a good option if you don't have your own website. The benefit of this approach would be that people can create PRs and issues for your tutorials.

Popular publishing platforms are [Medium.com](http://Medium.com), [Dev.to](http://Dev.to), [Hackernoon.com](http://Hackernoon.com), and [FreeCodeCamp.com](http://freeCodeCamp.com). [Mirror.xyz](http://Mirror.xyz) is an excellent web3 publishing platform that you should look into.

If you are creating content that uses the Celo blockchain, you can also submit it to the Celo Sage program and get it published on the Celo websites. More on that in the conclusion.

**How can I promote my tutorial?**

If you publish on platforms like [Medium.com](http://Medium.com) etc. you will already have an audience for your content that you won't have when publishing on your own website. You should consider this when making the decision of where to publish.

After publishing, try to find forums, Telegram channels, or Reddit communities that could be relevant to your content.

You can then share it on social media platforms like Twitter, LinkedIn, or Facebook, to get additional views. Try to ask an influencer with many followers on the platform if they might share it too.

**How can I attract a bigger audience after publishing and promoting it?**

Think about converting your written tutorial into a video tutorial. For a lot of beginners, video tutorials are very attractive. You can just record your screen doing your tutorial and later add a video commentary.

Continuously improve upon your tutorial. Especially if you got initial traction, you could stay relevant by updating the tutorial to new versions of technology used and updating the FAQ section. If you have your tutorial as a markdown file on GitHub, you can also allow people to create PRs and help you update the content.

**I still need to decide on what topic to create a tutorial. Do you have ideas?**

If you are building something with the Celo technology, look at this [doc](https://s3-ap-southeast-1.amazonaws.com/he-public-data/2.0%20Build%20with%20Celo%20Hackathon%20Inspiration11ee984.pdf), where they shared some ideas on things that they would love to see.

**What is the best technology that I should use for building with Celo?**

Have a look at Celo's [developer section](https://docs.celo.org/developer) in their docs. Currently, the [Celo Composer](https://github.com/celo-org/celo-composer) is the best way for beginners to create dapps. But look into the documentation and look for the Celo tooling that is most actively maintained, with the most current commits. For creating, testing, and deploying contracts, we recommend using [Hardhat](https://hardhat.org/).
