# Unity Setup for EDU & Research Use cases

This is a document I'm creating that encompasses all of my previous Unity experiences down to the same set of core needs with current solutions and possible future workflows.

Why?

I need a way to build in workflows that can grow and will last for the next 5 years without redoing everything all of the time.

## Unity Development Writing Code

This is really straight forward: Unity Package Manager and assembly definition files that align to use. We then host these packages under an open source license agreement.

## Unity Asset & Content Management

Unity Addressables broken out via the workflows that Trent and Jackson have worked out. This doesn't address how we actually manage our 2D/3D content, this is just how we manage it internal to Unity. Artists and content creators aren't directly creating content in Unity. They are creating content in Blender, Maya, Adobe Products, etc. we aren't managing any of this - zip/zero - and we should be.

## Building and Deploying - CI/CD

Below is going to be a list of sub topics tied to all areas of deployment and/or user management that should be agnostic of Unity but can also be Unity via their game services. This is usually all summed up as CI/CD = continuous integration and continuous deployment. Almost all of the services and/or issues mentioned further is part of this process but I will break them out as separate pieces in this document.

We already have the repository nailed down: GitHub no matter what. Now it's a question of how do we go from building and updating a 'build' to getting that build through its test and processes directly to your user. Unity is finally building these tools and to me they look a lot like PlayFab which is another service that builds these things in and we could use PlayFab as an overall solution which is a set of tools that are wrapped around Microsoft Azure services.

## User Authentication

How are we verifying our users and how are we then using that information to link to game service content. We aren't doing any of this but there are a lot of services out there. In most cases we can piggy back off Apple, Google, &/or Meta as 99% of everyone probably has one of those accounts. We can also pay for other services to manage it for us who they then piggy back off the big players but we provide 'our own way' that utilizes it. This is just like every other service you've ever used - you go to login and you have the option "login with Apple" etc.

**Going forward** we need to do this asap and for everything we publish. If we are really serious about data we have to manage user identification from the beginning.

## Data

What are we storing here? Are we talking about a true agnostic content experience - in which digital content can be moved between different Unity games/experiences?

### Data Storage and Types

When we say data we need to be very specific and below is a list of what I think are the high categories that then all have different needs and/or requirements.

- Game Data
  - Content from a game that the player earns and/or deals with progression
  - e.g. inventory items, unlocks, character skins, etc.
  - this could be directly tied to visuals, it could be textual, it could be a lot of things but at the heart it's an index that points to a type
    - User has ID#1001 which when we look it up points to a bucket storage that is part of an addressable asset bundle
  - Our data assets tied what the users are doing
    - e.g. Modules
- Educational Research Data
  - Data that deals with all things research
  - This is always going to change but we can probably hammer out some standards
  - Relational and non-relational types
  - e.g. could be something like raw eye tracking data
- User Data
  - e.g. data tied to our user and/or accounts
    - school division
    - teacher
    - grade etc.
    - restrictions tied to age under 13 vs over 13
- Virginia EDU standards
  - Data that directly relates to some sort of VA EDU need
  - All relational and/or just a big look-up table
  - Syncs with our game data and/or works with it
  - do we host this or do we api it back to the state
    - the state probably doesn't have this in a database API format yet

That's just the high level stuff, there's a ton of nuances here, and managing this is an absolute job. Ideally we take our solutions and park them in a big service like Azure - we then write our own API to access that data so we have a way to let other people ping/use our services to do whatever it is they want with our data. The best example I can think of here is how you'd incorporate our data back into an LMS. We wouldn't want to write a bunch of one-of solutions for various LMS - but instead develop and support our own API so then it doesn't matter *what* service needs our data integration, it just uses the API to go get it.

## Learning Management Systems

Once we have data stored in our various services we probably need a way to bring that data back into an LMS. At this point we would then actually need our own API for our data.

## Target Users

We know that at the EDU level we are dealing with sort of 4 high level tiers of users and currently we are only hitting one of them.

- Students
  - Access: Via the Game itself
- Teachers
  - Access: Via the Game itself and an online portal
- Administrators
  - Access: Online Portal
- School Districts
  - Access: Online Portal

To really do this *right* we need to bring in web developers and we need to build a solution that is basically a graphical interface that interacts with our data as mentioned above.

## All the Major Pieces

- Unity Engine
  - Core Engine Script Systems: Package Manager
  - Core Engine Content Systems: Addressable Asset System
- Web infrastructure for online Portal
- Data and Database Architecture
  - API services
- User Authentication
- CI/CD services
  - Repository Management: GitHub
  - Q&A Testing: ?
  - Game Build Analytics
  - Game Deployment Integration with Distribution Platforms (Steam/iOS/Google/Meta/Custom WebGL)
- Content Delivery Network (CDN)
  - Might be Deployment based e.g. using a Google Service for Android Play
  - Managing this content before it's packaged
