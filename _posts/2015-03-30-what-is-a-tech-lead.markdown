---
layout: post
title:  "What is a tech lead?"
date:   2015-03-30 08:20:43
categories: engineering development leadership
comments: true
---

The term tech lead seems to be used in wider and wider circles, with each company defining the role in different ways. But what is a tech lead, and what are their responsibilities? To my mind, the responsibility flows in three directions:

1. Upwards: Responsibile to the directors within amido for delivering the project to a high technical standard, an architecture that adheres to the company's core principles and a solution that befits the budget and scope
2. Downwards: Ensuring the team follows rigourous coding practices by laying out the framework for them to do so. Ensuring TDD is used and that the acceptance tests are kept up to date.
3. Outwards: To the client. Ensuring their internal infrastructure is able to support the solution as designed, that they feel engageged in the creation and delivery of their project from a technical level, and that they have adequate access to see their work progressing steadily.

Within Amido the tech lead is the most senior technical consultant assigned to a project and is ultimately the person who hands the code over to the client. They are responsible for definining the architecture and assuring sign off from the other tech leads, as well as engineering standards to be followed by the development team.

I'm personally very keen to ensure that we set out our patterns and code base as early as possible in order to maximise the the team's ability to extend and maintain the code base. The tech lead's job is to look ahead and build a solution that takes the future into account while not holding back development work. This can be a bit of a juggling act sometimes, with some observers feeling that work is being done that is not of direct benefit in terms of features to the client, but being up front and honest about the motivations can usually get clients on board with such work.

The final piece of the puzzle for me is to ensure that the financial implications of any solution are considered. One example from my own experience is to consider high usage rates of a system as a pointer to high costs if not caught soon enough. Large numbers of files with a high number of requests can quickly become very expensive, meaning compression and minification of static assets takes on more meaning that simply performance. It means cold, hard cash to clients.