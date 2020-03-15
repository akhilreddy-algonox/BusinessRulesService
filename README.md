---
title: 'BusinessRules documentation'
disqus: Akhil
---

Business Rules
===
![build](https://img.shields.io/appveyor/build/:user/:repo)
![chat](https://img.shields.io/discord/:serverId.svg)

## Table of Contents

[TOC]

## About (Why?)
As a software system grows in complexity and usage, it can become burdensome if every change to the logic/behavior of the system also requires you to write and deploy new code. The goal of this business rules engine is to provide a simple interface allowing anyone to capture new rules and logic defining the behavior of a system, and a way to then process those rules on the backend.

## Overall Flow
![alt FlowChart](https://github.com/akhilreddy-algonox/BusinessRulesService/blob/master/mermaid-diagram-20200316013849.svg)


## Configuration Tables
1) **sequence_rule_data**

    1) <em>rule_string</em> - The rule string that needs to be executed.<br>
   2) <em>Description</em> - Description of a rule.<br>
   3) <em>rule_id</em> - A unique id for each rule to be referenced by.<br>
   4) <em>next_if_success</em> -The rule id to follow if the current rules gives the output as True. <br>
   5) <em>next_if_failure</em> -The rule id to follow if the current rules gives the output as False.<br>
   6) <em>group</em> -The group of the rule.<br>
   
   
   ![alt sequence_rule_data table](https://github.com/akhilreddy-algonox/BusinessRulesService/blob/master/Annotation%202020-03-16%20020618.png)

2) **data_sources**
    1) <em>case_id_based</em> -The data table which are to be considered where the case_id is known.<br>
    2) <em>master</em> -The data table which are to be considered where the case_id is not known.<br>

    ![alt datasources table](https://github.com/akhilreddy-algonox/BusinessRulesService/blob/master/datasources.png)



## Rule Strings
Rulestrings are objects which are designed for business rule engine.
Considering an analogy, you can think rule strings as byte code for business rule engine.

## Creating RuleStrings

If you are a total beginner to this, start here!

1. Visit hackmd.io
2. Click "Sign in"
3. Choose a way to sign in
4. Start writing note!

Some Examples
---

```gherkin=
Feature: Guess the word

  # The first example has two steps
  Scenario: Maker starts a game
    When the Maker starts a game
    Then the Maker waits for a Breaker to join

  # The second example has three steps
  Scenario: Breaker joins a game
    Given the Maker has started a game with the word "silky"
    When the Breaker joins the Maker's game
    Then the Breaker must guess a word with 5 characters
```
> I choose a lazy person to do a hard job. Because a lazy person will find an easy way to do it. [name=Bill Gates]


```gherkin=
Feature: Shopping Cart
  As a Shopper
  I want to put items in my shopping cart
  Because I want to manage items before I check out

  Scenario: User adds item to cart
    Given I'm a logged-in User
    When I go to the Item page
    And I click "Add item to cart"
    Then the quantity of items in my cart should go up
    And my subtotal should increment
    And the warehouse inventory should decrement
```

> Read more about Gherkin here: https://docs.cucumber.io/gherkin/reference/

## Decision Tree

## Appendix and FAQ

:::info
**Find this document incomplete?** Reach out to admin@algonox.com!
:::

###### tags: `Business Rules` `Documentation` `AlgonoX`
