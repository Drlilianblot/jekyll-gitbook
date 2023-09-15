# 7 - Code Documentation

## Introduction

When you write code, you write it for two primary audiences: your end-users and developers (including yourself) in your project team. Both audiences are equally important.

There is a surprising amount of passionate debates within the developer community regarding the usefulness or desirability of comments in source code. Should source code include significant comments or none at all or something in-between?

To date, I haven't been able to find a study exploring the benefit (or lack of) of commenting code, and its economic impact (positive or negative). Similarly, I could not find any study exploring the benefits and drawbacks of different standards and approaches to documenting code. In the remainder of the chapter, I will present some best practices as well as several standards used in the Python community.

But first of all, we should have a look at the debate on the use of comments in code, and explore both side of the argument. In his article, [Kunk](https://visualstudiomagazine.com/articles/2011/01/06/to-comment-or-not-to-comment.aspx) summarise his thoughts on both side of the argument. Kunk lists three points in favour of using comments.

* **It's important to communicate what the code SHOULD be doing.** \
  Comments are required to communicate the intent of the source apart from its functionality. When reading source code, it is extremely difficult to be certain as to what the original author intended. Comments should clearly communicate the developer's intent and if needed, an explanation as to how the source code algorithm accomplishes that intent.
* **Comments show respect for the next developer to read your code.** \
  Source code should be written in the way that you yourself would most like to encounter unfamiliar code. It should be well-structured with a clear logic flow, and be both efficient and effective. Comments enhance the readability of the code, so that its intent and approach are immediately apparent with a clean appearance.
* **Comments indicate potential problem areas to avoid.**\
  Comments should mention factors that may be of concern for the developer or tester. Boundary conditions, valid argument ranges, and corner cases are all important factors to mention in comments for the benefit of future developers and testers.

In his column, he also lists three point against the use of comments in source code:&#x20;

* **Comments take time and have cost but do not influence runtime behaviour.** \
  Clearly, comments are not going to improve runtime performance, they are solely for the benefit of the developers. The creation of comment do take time, and may require additional maintenance when code is changed or re-factored. This obviously add an additional cost to the maintenance. Therefore, the comment must justify its cost by providing a benefit greater than its cost. Bad comments are an unnecessary cost.
* **Comments are not properly maintained.**\
  Under time pressure, comments are generally the last thing to be addressed (if at all) and may become out of sync with the current code.
* **Comments may simply be incorrect.**\
  Sometimes comments are written by developers that misunderstand the code and reinforce that misunderstanding through incorrect or misleading text. The feeling is that bad comments are worse than no comments.

Kunk concluded that he was generally in the camp in favour of documenting code. He added that comments have values and justifies the cost. However, he also warn that comments need to be maintained with the same diligence as executable source code.

In is column, [Vogel](https://visualstudiomagazine.com/articles/2013/06/01/roc-rocks.aspx) agrees on the first point from Kunk, that is comments should explain the "why" of the code and stop there. He extended the usefulness of comments to includes description of how inputs and outputs of a method/function are related, and a list of expected "side effects". \
What does he mean by "side effect"? \
A "side effect" is any result from executing the code that isn't reflected in the values that the code returns. For example, deleting a record, sorting a mutable object such as a `list` passed in the parameters.

Vogel also argues that comments (apart from end-user documentation) should be replaced by a ROC (Really Obvious Code) approach, supported by Test Driven Development (TDD) or at least a set of automated test suits, something that will be discussed later in the book.

So where do I stand on the issue of comments. I believe that comments are necessary, but one must strive to write good/useful comments. There are several reasons for this:&#x20;

* **Not all programmers can write really obvious code.** \
  In addition, judging whether code is obvious is a subjective call. What is obvious to one person might be cryptic for another. This is especially true if a novice programmer reads the code of an experienced developer. [Mertz](https://realpython.com/documenting-python-code/#commenting-vs-documenting-code) illustrates this point brilliantly. "If you’re like me, you’ve probably opened up old codebases and wondered to yourself, _What in the world was I thinking?_ If you’re having a problem reading your own code, imagine what your users or other developers are experiencing when they’re trying to use or contribute to your code."
* **Comments are not just for code.** \
  They can document important program information such as author, date, license, and copyright details. Although it should be noted this might be a mute point since version control systems are readily available.
* **Comments can be place holders for future work.** \
  This is a useful way to create an outline for a large program. Some Integrated Development Environment (IDE) uses tag within comments to create to-do lists.

In summary, both authors agree that good comments are useful and bad comments should be avoided at all costs. So what are good and bad comments?

Finally, a key message to get from this introduction is perfectly summarised by a quote from ["The Elements of Programming Style"](http://www2.ing.unipi.it/\~a009435/issw/extra/kp\_elems\_of\_pgmng\_sty.pdf):

> Don’t comment bad code -- rewrite it. (Brian W. Kernighan and P. J. Plaugher)

## Why Documenting Your Code Is So Important

Conversely, I’m sure you’ve run into a situation where you wanted to do something in Python and found what looks like a great library that can get the job done. However, when you start using the library, you look for examples, write-ups, or even official documentation on how to do something specific and can’t immediately find the solution.

After searching, you come to realize that the documentation is lacking or even worse, missing entirely. This is a frustrating feeling that deters you from using the library, no matter how great or efficient the code is. Daniele Procida summarized this situation best:

> It doesn’t matter how good your software is, because if the documentation is not good enough, people will not use it. (Daniele Procida)
