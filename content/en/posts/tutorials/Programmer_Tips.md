# How to be a Programmer: Community Version

Original book link: https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/

## Beginner
### [How to Optimize Loops](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Personal-Skills/07-How-to-Optimize-Loops.html)
Here are some suggestions:
* Remove floating point operations.
* Don't allocate new memory blocks unnecessarily.
* Fold constants together.
* Move I/O into a buffer.
* Try not to divide.
* Try not to do expensive typecasts.
* Move a pointer rather than recomputing indices.

### [How to Deal with I/O Expense](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Personal-Skills/08-How-to-Deal-with-IO-Expense.html)
Representations can often be improved by a factor of two or three from their first implementation. 
Techniques for doing this include using a binary representation instead of one that is human readable, 
transmitting a dictionary of symbols along with the data so that long symbols don't have to be encoded, 
and, at the extreme, things like **Huffman encoding**.

### [How to Manage Memory](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Personal-Skills/09-How-to-Manage-Memory.html)
Space that needs to persist beyond the scope of a single subroutine is often called **heap allocated**. A chunk of memory is useless, hence garbage, when nothing refers to it. Depending on the system you use, you may have to explicitly deallocate memory yourself when it is about to become **garbage**. More often you may be able to use a system that provides a **garbage collector**.

But even with garbage collection, you can fill up all memory with garbage. A classic mistake is to use a hash table as a cache and forget to remove the references in the hash table. Since the reference remains, the referent is non-collectable but useless. This is called a memory leak. You should look for and fix **memory leaks** early. If you have long running systems memory may never be exhausted in testing but will be exhausted by the user.

### [How to Deal with Intermittent Bugs](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Personal-Skills/10-How-to-Deal-with-Intermittent-Bugs.html)
The intermittent bug is a cousin of the 50-foot-invisible-scorpion-from-outer-space kind of bug. This nightmare occurs so rarely that it is hard to observe, yet often enough that it can't be ignored. You can't debug because you can't find it.

### [How to Conduct Experiments](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Personal-Skills/12-How-to-Conduct-Experiments.html)
First, try to be very clear about your hypothesis, or the assertion that you are trying to test. It also helps to write the hypothesis down, especially if you find yourself confused or are working with others.

You will often find yourself having to design a series of experiments, each of which is based on the knowledge gained from the last experiment. Therefore, you should design your experiments to provide the most information possible. Unfortunately, this is in tension with keeping each experiment simple - you will have to develop this judgement through experience.

### [How to Estimate Programming Time](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Team-Skills/02-How-to-Estimate-Programming-Time.html)
When not possible to take the time for some investigation, you should first establish the meaning of the estimate very clearly. Restate that meaning as the first and last part of your written estimate. Prepare a written estimate by de-constructing the task into progressively smaller subtasks until each small task is no more than a day; ideally at most in length. 

The most important thing is not to leave anything out. For instance, documentation, testing, time for planning, time for communicating with other groups, and vacation time are all very important. If you spend part of each day dealing with knuckleheads, put a line item for that in the estimate. This gives your boss visibility into what is using up your time at a minimum, and might get you more time.

### [How to Find Out Information](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Team-Skills/03-How-to-Find-Out-Information.html)
The nature of what you need to know determines how you should find it.

### [How to Utilize People as Information Sources](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Team-Skills/04-How-to-Utilize-People-as-Information-Sources.html)
Respect every person's time and balance it against your own. Asking someone a question accomplishes far more than just receiving the answer. The person learns about you, both by enjoying your presence and hearing the particular question. You learn about the person in the same way, and you may learn the answer you seek. This is usually far more important than your question.

### [How to Document Wisely](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Team-Skills/05-How-to-Document-Wisely.html)
It means:
* Writing code knowing that someone will have to read it;
* Applying the **golden rule** : `Do unto others as you would have them do unto you`;
* Choosing a solution that is straightforward, even if you could get by with another solution faster;
* Sacrificing small optimizations that obfuscate the code;
* Thinking about the reader and spending some of your precious time to make it easier on her; and
* Not ever using a function name like `foo`, `bar`, or `doIt`!

### [How to Work with Poor Code](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Team-Skills/06-How-to-Work-with-Poor-Code.html)
This is a good time to document, even if it is only for yourself, because the act of trying to document the code will force you to consider angles you might not have considered, and the resulting document may be useful. 

While you're doing this, consider what it would take to rewrite some or all of the code. Would it actually save time to rewrite some of it? Could you trust it better if you rewrote it? Be careful of arrogance here. If you rewrite it, it will be easier for you to deal with, but will it really be easier for the next person who has to read it? If you rewrite it, what will the test burden be? Will the need to re-test it outweigh any benefits that might be gained?

### [How to Recognize When to Go Home](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/1-Beginner/Team-Skills/10-How-to-Recognize-When-to-Go-Home.html)
There are four defences against this:
* Communicate as much as possible with everyone in the company so that no one can mislead the executives about what is going on,
* Learn to estimate and schedule defensively and explicitly and give everyone visibility into what the schedule is and where it stands,
* Learn to say no, and say no as a team when necessary, and
* Quit if you have to.

## Intermediate
### [How to Stay Motivated](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Personal-Skills/01-How-to-Stay-Motivated.html)
This has practical and important consequences. If programmers are asked to do something that is not beautiful, useful or nifty, they will have low morale. There's a lot of money to be made doing ugly, stupid, and boring stuff; but in the end, fun will make the most money for the company.

Obviously, there are entire industries organized around motivational techniques, some of which apply here. The things that are specific to programming that I can identify are:
* Use the best language for the job.
* Look for opportunities to apply new techniques, languages and technologies.
* Try to either learn or teach something, no matter how small, in each project.

### [How to Tradeoff Time vs. Space](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Personal-Skills/03-How-to-Tradeoff-Time-vs-Space.html)
In designing or understanding an algorithm, the amount of time it takes to run is sometimes a function of the size of the input. When that is true, we can say an algorithm's worst/expected/best-case running time is 'n log n' if it is proportional to the size ($n$) times the logarithm of the size. The notation and way of speaking can be also be applied to the space taken up by a data structure.

Time (processor cycles) and space (memory) can be traded off against each other. Engineering is about compromise, and this is a fine example. It is not always systematic. In general, however, one can save space by encoding things more tightly, at the expense of more computation time when you have to decode them. You can save time by caching, that is, spending space to store a local copy of something, at the expense of having to maintain the consistency of the cache. You can sometimes save time by maintaining more information in a data structure. This usually costs a small amount of space, but may complicate the algorithm.

### [How to Balance Brevity and Abstraction](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Personal-Skills/05-How-to-Balance-Brevity-and-Abstraction.html)
Occasionally, one sees a mistake made by enthusiastic idealists: at the start of the project a lot of classes are defined that seem wonderfully abstract and one may speculate that they will handle every eventuality that may arise. As the project progresses and fatigue sets in, the code itself becomes messy. Function bodies become longer than they should be. The empty classes are a burden to document that is ignored when under pressure. The final result would have been better if the energy spent on abstraction had been spent on keeping things short and simple. This is a form of speculative programming. I strongly recommend the article 'Succinctness is Power' by Paul Graham.

### [How to Learn New Skills](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Personal-Skills/06-How-to-Learn-New-Skills.html)
If you lead people, understand how they learn and assist them by assigning them projects that are the right size and that exercise skills they are interested in. Don't forget that the most important skills for a programmer are not the technical ones. Give your people a chance to play and practice courage, honesty, and communication.

### [Learn to Type](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Personal-Skills/07-Learn-to-Type.html)
Learn to touch-type. This is an intermediate skill because writing code is so hard that the speed at which you can type is irrelevant and can't put much of a dent in the time it takes to write code, no matter how good you are.

### [Heavy Tools](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Personal-Skills/10-Heavy-Tools.html)
To my mind right now some of the best heavy tools are:
* Relational Databases,
* Full-text Search Engines,
* Math libraries,
* OpenGL,
* XML parsers, and
* Spreadsheets.

### [How to analyze data](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Personal-Skills/11-How-to-analyze-data.html)
However, the process is not over yet, because you (the programmer) even after this thorough process of data refinement, are required to analyze data to perform the task in the best possible way. The bottom line of your task is the core message of Niklaus Wirth, the father of several languages. "Algorithms + Data Structures = Programs." There is never an algorithm standing alone, doing something to itself. Every algorithm is supposed to do something to at least one piece of data.

### [How to Manage Third-Party Software Risks](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Team-Skills/02-How-to-Manage-Third-Party-Software-Risks.html)
A project often depends on software produced by organizations that it does not control. There are great risks associated with third party software that must be recognized by everyone involved.

### [How to Disagree Honestly and Get Away with It](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Team-Skills/05-How-to-Disagree-Honestly-and-Get-Away-with-It.html)
Whether the decision is reversed or not, you must remember that you will never be able to say ‘I told you so!’ since the alternate decision was fully explored.

### [How to Manage Software System Dependence](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Judgment/02-How-to-Manage-Software-System-Dependence.html)
However, each component brings with it some problems:
* How will you fix bugs in the component?
* Does the component restrict you to particular hardware or software systems?
* What will you do if the component fails completely?

### [How to Decide if Software is Too Immature](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Judgment/03-How-to-Decide-if-Software-is-Too-Immature.html)
Here are ten questions you should ask yourself about it:
* Is it vapour? (Promises are very immature).
* Is there an accessible body of lore about the software?
* Are you the first user?
* Is there a strong incentive for continuation?
* Has it had a maintenance effort?
* Will it survive defection of the current maintainers?
* Is there a seasoned alternative at least half as good?
* Is it known to your tribe or company?
* Is it desirable to your tribe or company?
* Can you hire people to work on it even if it is bad?

### [How to Evaluate Interviewees](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Judgment/06-How-to-Evaluate-Interviewees.html)
You should, at a minimum, give the candidate the equivalent of an oral examination on the technical skills for two hours. With practice, you will be able to quickly cover what they know and quickly retract from what they don't know to mark out the boundary. Interviewees will respect this. I have several times heard interviewees say that the quality of the examination was one of their motivations for choosing a company. Good people want to be hired for their skills, not where they worked last or what school they went to or some other inessential characteristic.

Finally, interviewing is also a process of selling. You should be selling your company or project to the candidate. However, you are talking to a programmer, so don't try to colour the truth. Start off with the bad stuff, then finish strong with the good stuff.

### [How to Know When to Apply Fancy Computer Science](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Judgment/07-How-to-Know-When-to-Apply-Fancy-Computer-Science.html)
The three most important considerations for the potential computer science technique are:
* Is it well encapsulated so that the risk to other systems is low and the overall increase in complexity and maintenance cost is low?
* Is the benefit startling (for example, a factor of two in a mature system or a factor of ten in a new system)?
* Will you be able to test and evaluate it effectively?

### [How to Talk to Non-Engineers](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/2-Intermediate/Judgment/08-How-to-Talk-to-Non-Engineers.html)
Non-programmers can understand technical things but they do not have the thing that is so hard even for us - technical judgement. They do understand how technology works, but they cannot understand why a certain approach would take three months and another one three days. (After all, programmers are anecdotally horrible at this kind of estimation as well.) This represents a great opportunity to synergize with them.

## Advanced
### [How to Tell the Hard From the Impossible](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Technical-Judgment/01-How-to-Tell-the-Hard-From-the-Impossible.html)
It is our job to do the hard and discern the impossible. From the point of view of most working programmers, something is impossible if either it cannot be grown from a simple system or it cannot be estimated. By this definition, what is called research is impossible. A large volume of mere work is hard, but not necessarily impossible.

### [How to Utilize Embedded Languages](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Technical-Judgment/02-How-to-Utilize-Embedded-Languages.html)
Embedding a programming language into a system has an almost erotic fascination to a programmer. It is one of the most creative acts that can be performed. It makes the system tremendously powerful. It allows you to exercise her most creative and Promethean skills. It makes the system into your friend.

### [Choosing Languages](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Technical-Judgment/03-Choosing-Languages.html)
In other cases the very real benefit of unity among the team, and to some extent with a larger community, precludes choice on the part of the individual. Often managers are driven by the need to be able to hire programmers with experience in a given language. No doubt they are serving what they perceive to be the best interests of the project or company, and must be respected for that. However, I personally believe this is the most wasteful and erroneous common practice you are likely to encounter.

### [How to Understand the User](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Compromising-Wisely/02-How-to-Understand-the-User.html)
* The user generally makes short pronouncements.
* The user has their own job; they will mainly think of small improvements in your product, not big improvements.
* The user can't have a vision that represents the complete body of your product users.

### [How to Develop Talent](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/01-How-to-Develop-Talent.html)
Try to get each team member to buy in and be well motivated. Ask each of them explicitly what they need to be well-motivated if they are not. You may have to leave them dissatisfied, but you should know what everybody desires.

### [How to Choose What to Work On](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/02-How-to-Choose-What-to-Work-On.html)
You balance your personal needs against the needs of the team in choosing what aspect of a project to work on. You should do what you are best at, but try to find a way to stretch yourself not by taking on more work but by exercising a new skill. Leadership and communication skills are more important than technical skills. If you are very strong, take on the hardest or riskiest task, and do it as early as possible in the project to decrease risk.

### [How to Get the Most From Your Team-mates](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/03-How-to-Get-the-Most-From-Your-Teammates.html)
Praise frequently rather than lavishly. Especially praise those who disagree with you when they are praiseworthy. Praise in public and criticize in private; with one exception: sometimes growth or the correction of a fault can't be praised without drawing embarrassing attention to the original fault, so that growth should be praised in private.

### [How to Divide Problems Up](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/04-How-to-Divide-Problems-Up.html)
There is a certain danger in this given that people will become bored as they build upon their strengths and never improve their weaknesses or learn new skills. However, specialization is a very useful productivity tool when not overused.

### [How to Handle Boring Tasks](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/05-How-to-Handle-Boring-Tasks.html)
Sometimes it is not possible to avoid boring tasks that are critical to the success of the company or the project. These tasks can really hurt the morale of those that have to do them. The best technique for dealing with this is to invoke or promote Larry Wall's programmer's virtue of Laziness. Try to find some way to get the computer to do the task for you or to help your team-mates do this. Working for a week on a program to do a task that will take a week to do by hand has the great advantage of being more educational and sometimes more repeatable.
If all else fails, apologize to those who have to do the boring task, but under no circumstances allow them to do it alone. At a minimum assign a team of two to do the work and promote healthy teamwork to get the task done.

### [How to Communicate Well](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/08-How-to-Communicate-Well.html)
To communicate well, you have to recognize how hard it is. It is a skill unto itself. It is made harder by the fact that the persons with whom you have to communicate are flawed. They do not work hard at understanding you. They speak poorly and write poorly. 

They are often overworked or bored, and, at a minimum, somewhat focused on their own work rather than the larger issues you may be addressing. One of the advantages of taking classes and practising writing, public speaking, and listening is that if you become good at it you can more readily see where problems lie and how to correct them.

### [How to Tell People Things They Don't Want to Hear](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/09-How-to-Tell-People-Things-They-Dont-Want-to-Hear.html)
The best way to tell someone about a problem is to offer a solution at the same time. The second best way is to appeal to them for help with the problem. If there is a danger that you won't be believed, you should gather some support for your assertion.

### [How to Deal with Managerial Myths](https://braydie.gitbooks.io/how-to-be-a-programmer/content/en/3-Advanced/Serving-Your-Team/10-How-to-Deal-with-Managerial-Myths.html)
* More documentation is always better. (They want it, but they don't want you to spend any time on it.)
* Programmers can be equated. (Programmers vary by an order of magnitude.)
* Resources can be added to a late project to speed it. (The cost of communication with the new persons is almost always more taxing than helpful.)
* It is possible to estimate software development reliably. (It is not even theoretically possible.)
* Programmers' productivity can be measured in terms of some simple metric, like lines of code. (If succinctness is power, lines of code are bad, not good.)

## Reference
```
How to be a Programmer: Community Version
Robert L. Read with Community
Copyright 2002, 2003, 2016 Robert L. Read
```

## License
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
  <img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" />
</a>
<br />
This work is licensed under a 
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">
  Creative Commons Attribution-ShareAlike 4.0 International License
</a>.
