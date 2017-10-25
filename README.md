# Midterm

## Pick a Project

- Wiki Map
- Card Game
- Decision Maker
- Smart TODO List
- Resource Wall
- Schoodle
- Food Pick-Up Ordering

## Planning

### User Stories

> Important!

Use google docs and write out stories that describe the roles, goals and benefits. `As a _____, I want to _____, Because _____.`

A user scenario describes a context, the action taken, and the result. `Given _____, When _____, Then _____.`

Read this article, it only takes a few minutes and it is a good process for thinking about user stories.

[https://medium.com/@jonatisokon/a-framework-for-user-stories-bc3dc323eca9](https://medium.com/@jonatisokon/a-framework-for-user-stories-bc3dc323eca9)

### Features

Decide what your competative advantage is. Focus on that.

All of the features that you need to prove your method works need to be there. This is an MVP, minimum viable product. Wouldn't it be cool if we focused on the most important things.

You don't need to prove you can make a login flow. We've done that already. You would never do this in production, but for development you can setup a route to log you in as any user.

```javascript
app.get('/login/:id', (request, response) => {
  request.session.user_id = request.params.id;
  resonse.redirect('/');
});
```


### ERD

> Important!

https://www.draw.io/

Where are the relationships? Get this reviewed by a mentor.

Tables are nouns, they can be taken right from User Stories.

Follow conventions:

- Table names are plural
- Primary key is `id`
- Foreign key is `<table>_id`

### Routes

Follow conventions:

- Browse/List/Index: GET /photos
- Create/Add: POST /photos
- Read/Show: GET /photos/:id
- Update/Edit: PUT /photos/:id
- Remove/Destroy: DELETE /photos/:id

### Wireframe

> Important!

You need to define where the data that you have chosen to collect is going to go on the pagse you can display.

- [Invision](https://www.invisionapp.com/)
- [Moqups](https://moqups.com/)
- [Balsamiq](https://balsamiq.com/)
- [Wireframe.cc](https://wireframe.cc/)
- [Mockingbird](https://gomockingbird.com/)

### Design

Design is important. Allow it to highlight your strengths but don't focus on it.

Fonts

Use only one or two fonts.

- [https://fonts.google.com/](https://fonts.google.com/)

[Font vs Typeface](http://mindgruve.com/blog/advertising/typeface-vs-font-what-is-the-difference) what is the difference?

Colours

With the tools available it is easy to choose colours that go well together.

- [https://color.adobe.com/](https://color.adobe.com/)
- [https://flatuicolors.com/](https://flatuicolors.com/)
- [https://coolors.co/](https://coolors.co/)
- [http://colormind.io/](http://colormind.io/)

Inspiration

- [https://dribbble.com/](https://dribbble.com/)

CSS Frameworks

In no particular order.

- [Skeleton](http://getskeleton.com/)
- [Bulma](https://bulma.io/)
- [Bourbon + Neat](https://neat.bourbon.io/)
- [Foundation](https://foundation.zurb.com/)
- [Bootstrap](http://getbootstrap.com/)
- [Groundwork](https://groundworkcss.github.io/)
- [Semantic UI](https://semantic-ui.com/)


## Git

Use good git practices. Please.

- Clone
- Branch
- Code & Test
- Checkout master
- Pull & Test
- Merge & Test
- Push
- Branch & Repeat


## Project Setup

Do this together.

- Setup GitHub repository with collaborators
- Clone github.com/lighthouse-labs/node-skeleton
- Follow instructions in node-skeleton README
- Make sure your app loads, check for console output
- Commit and push changes to GitHub
- Decide on team responsibilities

## Dividing Tasks

There is no perfect way to do this. You need to figure this out within your team. Here are some options.

Vertical

- Break the project out into features
- Prioritize the features
- Each developer would build a feature full stack

Horizontal

- Break the project down into technical domains
- One or more developers will be responsible for an entire domain
- Domains could be ui, api (routes), db

__Communication is critical no matter which way you divide the tasks.__

### Trello

Use this to plan your tasks. Everyone should sign up, someone creates a board and invites the rest of the team.

## Communication

- Slack
- What's App
- Skype
- appear.in

Just pick one you all agree on. Set expectations and meet them. If you need help, ask for it.

## Starting to Code

Pair programming can be a great way to get started.

### Browser

Start with a static page.

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="description" content="<fill this in>">
    <meta name="author" content="<fill this in>">

    <style>
    </style>
  </head>
  <body>
  </body>
</html>
```

> See sample in `start.html`.

You can put all of the structure and styles for a page into page.html. Once you feel comfortable, make these into templates. Only start coding the EJS or jQuery JavaScript portion after the style and structure is solid.

Use the static structure to understand how to break your layout into reusable pieces. This will help you break your client code into functions or your template code into partials.

Decide on css naming as a team.

User placeholders for text and images.

- http://fillmurray.com
- http://placekitten.com
- http://meettheipsums.com
- https://loremipsumgenerator.com/

Make sure to test your layouts with a lot of data, and don't alway use 'good' data.

### Node

Setup your database schema by creating one or more migrations. Setup some good test data in your seeds. Review your user stories and use the CLI make sure you can make the queries to satisfy them.

Once you are confident your queries work create the interface to the data you are retrieving from the database. The interface is usually the `Routes` that you design. Build this in small atomic steps. Use module exports and break your code up.

Let's say my user story is `As a user, I can view all of the photos of another user, because I want to see what they are about to eat for dinner.`. We need to figure out how to store this data necessary for this.

I need a photos table and a users table. Photos will belong to users. I've decided to store a link to a photo as a url. This way I can easily use placeholder images. Later on when I add the ability for a user to upload a photo I can update the database with a link to the uploaded photo.

```SQL
CREATE TABLE users (
  id SERIAL PRIMARY KEY NOT NULL,
  email varchar(255) NOT NULL,
  password varchar(32) NOT NULL
);

CREATE TABLE photos (
  id SERIAL PRIMARY KEY NOT NULL,
  url varchar(255),
  user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE
);

INSERT INTO users (email, password) VALUES ('first@user.com', '123456');
INSERT INTO users (email, password) VALUES ('second@user.com', '123456');

INSERT INTO photos (url, user_id) VALUES('http://www.fillmurray.com/g/200/300', 1);
INSERT INTO photos (url, user_id) VALUES('http://www.fillmurray.com/g/200/300', 1);
INSERT INTO photos (url, user_id) VALUES('http://www.fillmurray.com/g/200/300', 1);
INSERT INTO photos (url, user_id) VALUES('http://www.fillmurray.com/g/200/300', 2);
INSERT INTO photos (url, user_id) VALUES('http://www.fillmurray.com/g/200/300', 2);
INSERT INTO photos (url, user_id) VALUES('http://www.fillmurray.com/g/200/300', 2);
```

The route that I would use to view this would be `/users/:id/photos`. For the purposes of testing I would make this route return JSON, with the intention of having it render a template in the future.

```javascript
app.get('/users/:id/photos', (request, response) => {
  knex('photos').where('user_id', request.params.id).then(photos => {
    response.json(photos);
  });
});
```

In the case that I want to create a single page app, or even just query data from an api then this JSON response would be enough.

### Deployment

The two options are localhost and Heroku. If you are deploying to another server, then test this process early. You should only spend time on this if you have completed your most important features.
