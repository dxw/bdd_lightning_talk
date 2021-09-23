# Behaviour-Driven Development (BDD) #
Sept 23rd, 2021.

Note: I'm going to talk for a few minutes about BDD (behaviour driven development) -- and we're going to look at an example test presented in *different* ways.



## Definition ##

> User-centric acceptance test

Note: BDD is a style of writing automated tests which describes the *behaviour* of the system from the user's point of view.
We can characterise the tests produced as “user-centric acceptance tests”.



## Characteristics ##

- User focussed
- Aid to testing
- Executable documentation

Note:  These are artefacts which explain the value and behaviour of features from the end user's point of view. They help us keep user benefits at the front of our mind during development.
They often also have enduring value as 'plain English' testing scripts and documentation.
And as executable documentation -- automated tests which are part of our build pipeline -- they also help guard against bugs and regressions.
So what do these miracles of nature look like?



## Procedural ##

```ruby
scenario "can create an adjustment for an activity" do
  # setup
  # ...
  #
  # actions
  # ...
  #
  # assertions
  # ...
end
```

<a href='dxw/misc/bdd/procedural_example.html' style="font-size: 0.5em;">Procedural example</a>

Note: Is this BDD? I don't thnk so.

However, if you squint and concentrate you can see that we have 3 sections where we:

1. set up some objects and resource
2. perform some actions
3. make some assertions about the expected effects of those actions



## Expressive ##

```ruby
scenario "can create an adjustment for an activity" do
  given_an_active_report_exists
  and_i_am_looking_at_the_activity_financials_tab

  when_i_submit_the_new_adjustment_form_correctly
  then_i_expect_to_see_the_new_adjustment
end
```

<a href='dxw/misc/bdd/expressive_example.html' style="font-size: 0.5em;">Expressive example</a>

Note: now here we have a much more expressive version of the same test.

By wrapping the mechanics of the test in descriptive methods we make the purpose of this feature is much clearer. We use the familiar keywords of testing:

- Given
- When
- Then

to structure our setup, action and assertion phases.

And making our code more readable... (GO TO EXTRACT METHOD)

(AFTER WE'VE LOOKED AT EXTRACT METHOD)

Some of these methods we've extracted will be re-usable, and they ought to be easier to maintain -- but it's sufficient that they make the *behaviour* of the code clearer.

- We require an active report
- We get here via the financials tab
- We are able to create and review an adjustment

at a glance we know the purpose of this test.

BUT WE CAN DO BETTER..


## Extract method ##

> Turn the code fragment into a method whose name explains the purpose of the method

<cite style="font-size: 0.7em;">Refactoring Ruby (2010) by Fields, Harvey, Fowler</cite>

Note: .. and making our code more readable ... is business as usual.




## Behaviour-driven ##
  
```feature 
Feature: Delivery partner creates an adjustment via a form
  - So that BEIS can generate accurate reports for SID
  - As a Delivery partner
  - I want to adjust actual spends and refunds in historic periods in line with agreed   corrections

  Background:
    Given an active report exists
    And I am looking at the Activity -> Financials tab

  Scenario: can create an adjustment for an activity
    When I submit the new adjustment form correctly
    Then I expect to see the new adjustment
```

<a href='dxw/misc/bdd/behaviour-driven_example.html' style="font-size: 0.5em;">Behaviour-driven example</a>

Note: I think we can communicate the *purpose* of our work more clearly by adopting a richer separate layer for the documention function.

Yes -- there are really important mechanics involved in authorisation and validation, and in following links and clicking buttons, but what's most important here is the purpose of the feature, and the benefit it brings.

We have *errors* which we need to correct in order to produce a downstream *report*. Our way of fixing these errors is to create *adjusting* entries. And that is what we need to keep at the *forefront* of our minds as we develop, review and test the feature.



## User story ##

<img src="./dxw/misc/bdd/trello.png" style="max-width: 700px;" />

Note: Often a BDD style test maps really neatly onto our user story. And this means that your team -- your aceeptance testers: whether they be product owners, delivery managers, other developers -- these other team members can use the plain english part of your end-to-end test as a testing script.

This can be really powerful in reinforcing a shared understanding of the problem we are solving!

~~Yes -- there are really important mechanics involving in authorisation, validation, following links and clicking buttons, but the elements which are most important are the purpose of the feature, the value it brings. ~~



## Gherkin / Cucumber ##

<img src="./dxw/misc/bdd/outside_in.jpeg" />

Note: This separate layer of plain english documentation is of course Gherkin and is commonly used with cucumber.

Probably you are familiar with -- and use -- this "Outside-In" technique yourselves when driving your development through tests?

- we start off with an end-to-end test, exercising the entire system, poking at the inputs and observing theoutputs, using as little stubbing as possible

- we then drop down to unit tests which exercise small chunks of code (which may or may not be exercised in isolation)

By starting out with a description of the desired end-to-end behaviour -- starting at the OUTSIDE -- and then filling in the implementation details from INSIDE -> OUT, it's often easier to stay on track and come up with a good solution to the defined problem.

I hope I'm not the only person who often finds defining the problem really hard?



## Solutions to problems ##

OBJECTIVE
: the goal being frustrated

PROBLEM
: obstacle to achieving objective 

SOLUTION
: behaviour which delivers the remedy

Note: understanding problems and identifying remedies is difficult. We put our users first and think in terms of benefits and needs. But it's hard to write a correct user-story!



## Benefit-first ##

| FIRST     | SECOND      | THIRD        |
| ---       | ---         | ---          |
| why       | who         | what         |
| So that.. | As a...     | I want to... |

> So that I can x, as a y, I want to z

Note: One technique which I'm convinced helps -- is to always start by expressing the benefit, fix or solution which you want to bring. Don't let the tail wag the dog. Don't anticipate the solution. The *purpose* is the important part of the story. It's what we need to keep at the front of our minds. So put it *first*.



## OVER TO YOU ##

- your experiences?
- your opinions?
- your questions?



## Thanks ##



