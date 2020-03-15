
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
A rule is just a JSON object that gets interpreted by the business-rules engine. There are three keywords while writing rules. 

    1. rule_type -> static for functions, condition for conditional executions.
    2. function -> name of the function to be executed.
    3. parameters -> parameters required for the respective function.


1) **Rule Type:-**<br>
    Rule Type may be static, condition and table based on the user requirements.

    <em>Static</em>:
        It performs basic operations which are asked by the programmer.

    For eg.
    ```python
    {
      "rule_type": "static",
      "function": "Assign",
      "parameters": {
        "source": "input",
        "value": 5
      }
    }
    ```
    <em>Condition</em>:-
    It consists of two parts i.e condition and execution.
    If the first part is satisfied then the second part will get executed
    and comes out of the rule or else it goes to the next condition.

    For eg.
    ```python
    {
      "rule_type": "condition",
      "evaluations": [
        {
          "conditions": [
            some_rule, AND, other_rule
          ],
          "executions": [
            some_execution_rule, other_execution_rule
          ]
        },

        {
          "conditions": [
            different_rule, AND, other_rule
          ],
          "executions": [
            different_execution_rule, other_execution
          ]
        },

      ]
    }
    ```
    <em>Table</em>:-
    This type of rule is used to read a table that is     inside the main table column.

    ```python
    {
      "rule_type": "table",
      "table_name": "table_name",
      "column_name": "column_name",
      "evaluate_rule": {"rule":some_rule,
                          "start_row_index":5}
    }
    ```

2) **Function**<br>
    A function is a block of code that only runs when it is called. Some of them are Assign, Get Length, Select, etc...These functions are designed in such a way as the function name is given by the user, code gets call then the execution is done.
    
    Some available functions are:
    * Assign
    * AssignQ
    * CompareKeyValue
    * Select
    * Transform
    * GetLength
    * GetRange
            
3) **Parameters**

    *  You can pass data, known as parameters, into a function.
    *  Parameters are passed as an object.
    *  If source of the parameter is input_config then we are considering the value that are already in the database table that are read from datasources.
     For eg.
        ```python
            {
              "source": "input_config",
              "table": "ocr",
              "column": "Invoice Name"
            }
        ```
    *  If source of the parameter is input then we are considering the value as input from the use.<br>
    For eg.
        ```python
            {
              "source": "input",
              "value": "5",
            }
        ```
    *  If source of the parameter is rule then we are considering the value as the output by execting the rule.<br>
    For eg.
        ```python
        
            {
              "source": "rule",
              "value": tranform_rule,
            }
        
            transform_rule = {
              "rule_type": "static",
              "Function": "Transform",
              "Parameters": [
                {
                  "param": {
                    "source": "input_config",
                    "table": "ocr",
                    "column": "amt1"
                  }
                },
                {
                  "operator": "+"
                },
                {
                  "param": {
                    "source": "input_config",
                    "table": "ocr",
                    "column": "amt2"
                  }
                }
              ]
            }
            
        ```

Some Examples
---

###### Assign Rule
```python= 
{
  "rule_type": "static",
  "Function": "Assign",
  "parameters": {
    "assign_table": {
      "table": "ocr",
      "column": "total"
    },
    "assign_value": {
      "source": "rule",
      "value": Some_Rule
    }
  }
}
```



###### CompareKeyValue Rule
```python= 
{
  "rule_type": "static",
  "Function": "CompareKeyValue",
  "Parameters": {
    "left_param": {
      "source": "input_config",
      "table": "ocr",
      "column": "total_value"
    },
    "operator": "<",
    "right_param": {
      "source": "input",
      "value": 30
    }
  }
}

```


###### AssignQ Rule
```python= 
{
  "rule_type": "static",
  "Function": "Assign",
  "parameters": {
    "assign_table": {
      "table": "ocr",
      "column": "total"
    },
    "assign_value": {
      "source": "rule",
      "value": Some_Rule
    }
  }
}
```

> I choose a lazy person to do a hard job. Because a lazy person will find an easy way to do it. [name=True]


## Extending Functions`

## Decision Tree

## Appendix and FAQ

:::info
**Find this document incomplete?** Reach out to admin@algonox.com!
:::

###### tags: `Business Rules` `Documentation` `AlgonoX`
