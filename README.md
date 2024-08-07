# Digital Cafe

2024-04-29

This is the repository for the Digital Cafe walkthrough. Digital Cafe is the scenario that we use to teach students of ITMGT how to build a web application.

If you are a student aiming to complete the Digital Cafe assignment, please head to `doc/walkthrough` and go through each of the documents starting from 0001.

## Rationale behind choosing Django

This is the second version of Digital Cafe. The first one was written in Flask and used MongoDB as a database. We originally made both of these technology choices because they were _easy_. Flask made it possible to start a web app in a few lines of code and a single Python file. MongoDB's data model was very similar to a Python dictionary. Students would generally have an easier time getting on board both Flask and MongoDB, and for the first two years, it worked fine.

### Flask and Mongo are easy, but they come at a cost

The problem with both of these technology choices is that while easy, they produced code that was complex and difficult to maintain. Flask imposes very few opinions, if any, on how you should design your web application. This can be fine if you know what you're doing, but students (almost by definition) rarely do.

While Flask itself has remained stable, we have found that students rarely went on to build complex applications in Flask because they don't know how to implement new features. MongoDB was even worse for our learning objectives. I have written an [article](https://joeilagan.com/article/relational-data-ite) on why I grew to dislike recommending MongoDB to learners. That article focused mostly on the data model of MongoDB, but the database itself has also given Joben and I headaches as the instructions for installing it rapidly drifted away from what we'd written. Four years after the first version of Digital Cafe, we ended up having to allow and recommend students to use the free tier of MongoDB Atlas, their hosted cloud service. I predict that in another two years, five if I'm being generous, they will remove the free tier, as many other database vendors have done, leaving us with no option but to migrate to something that students can actually install. I figured that I may as well do the migration now.

### Django is hard, but it pays dividends

Django, in contrast with Flask, is much less _easy_ to get started with. It seems silly to some that the number of files in a Django project should be a reason to shy away from learning it, but compared to the single file of a Flask app, of course a larger project would intimidate a learner. I myself only returned to Django after spending four or five years with Flask and other microframeworks, but when I did return, it was immediately obvious to me (a microframework veteran at that point) that Django was the answer. Freedom in architecture is not necessarily good. Flask gives you a lot of freedom. As a beginner, you are free to tie your code into knots and make it impossible to understand or maintain. Django's much more structured approach to web development -- its framework, if you will -- almost forces you to use practices that are well-understood to protect the comprehensibility and maintainability of your code. If you stick to Django's use case, multi-page web applications that work with a database, Django will serve you well.

What I admire about Django as a framework is its internal consistency and its ability to avoid _complecting_ code. This word, complect, is one that I learned from Rich Hickey's talk on [simplicity](https://www.youtube.com/watch?v=SxdOUGdseq4). It means to weave or connect. You do not want this in your code. You want your code to stand alone, to be comprehensible alone, without needing to know the full context of the rest of the codebase. In general programming, that is why we use functions and try to avoid global variables. In the more specific area of web applications, Django imposes this philosophy on your code as well.

### On SQLite

I should also comment on my choice of database for the Django Digital Cafe: SQLite. It's not remarkable because it's a relational database. Django, true to its opinionated nature, gives you little choice other than to use a relational database. It's remarkable because it's _SQLite_. The toy database, the database that runs on phones and Raspberry Pi mini-computers. Can this seriously be the backbone of your application?

I kid; at this scale, of course it can. The nice thing about Django is that you are supposed to be able to tear out the relational database in the backend and replace it with any other. Since SQLite comes with Python, students won't need to install another database at all, never mind one as temperamental as Mongo. When (or more accurately if) the time comes, thanks to Django, students will also be able to rip out SQLite and replace it with Postgres.

Perhaps more significantly, we think that SQLite is both a) a good foundation for future learning, because it's a SQL database, and b) much less temperamental than Mongo. It's one of those boring but venerable technologies that will survive market cycles. SQLite itself is stable, open-source, and in the public domain, and the data model it uses (the relational data model) is the most important one in the modern tech industry. Maybe the best characteristic of SQLite from a course-teaching perspective is that you don't need to ask students to install a server. It's a gentle on-ramp to SQL.
