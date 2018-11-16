---
layout: post
comments: true
title:  "An Intuitive Explanation to Precision, Recall and Accuracy"
date:   2017-10-15 21:00:59 -0400
categories: machine-learning
---

Earlier this year, at an interview in New York I was asked about the recall and precision of one of my Machine Learning Projects. For a couple of minutes following that, the interviewer sat back and enjoyed the perplexed look on my face. I mean it’s not like I've never heard these terms before. I knew it involved some equations with True Positives. <i>Or was it False Negatives?</i>

I responded “My accuracy was 87%”, trying to slyly escape with a broad grin.

“Okay. But what was the precision and recall of your solution?”

![alt text][precision_recall_darts]

Needless to say, I didn't get the job. I never realized what the big deal was back then. I do now. Over the course of my summer internship as an <b>NLP Research Intern at ProQuest LLC</b>, I was forced to understand the business aspect of the project I was working on, and not simply apply python libraries blindly to some data. Today, I’d like to share some of that intuition with you.


So here’s the scenario :

You need to build a document classifier that splits documents into two buckets: <b>urgent</b> and <b>non-urgent</b>. Right now, there’s a team of qualified humans that read through each and every document and decide its urgency. Let’s assume that they get it right 100% of the time. Now if it’s a couple of documents every other day, you’re good. Scale that up to a couple 1,000 documents a week, and you need a solution. They call you in. You know that your model needs to do as well as the current team of super-humans;  only faster. If not replace, you at least need to optimize the current process.

Now comes the big question: "What do you optimize for?”

Accuracy would quite probably be your first answer, if not for my initial rant.

But now consider this:
Suppose you have 10 urgent documents and 90 non-urgent documents in your test document pool.

Your model has an accuracy of 90% on this dataset. What does that tell you?


<b>"ABSOLUTELY NOTHING."</b>


<u>Case 1:</u> You(<i> your model</i> ) got 80 of the non-urgent correct and labeled the remaining documents urgent. So you pass on 20 supposedly Urgent documents to the team( only half of which are actually urgent). Great! You didn’t miss any urgent document.

<u>Case 2:</u> You(<i> your model</i> )  marked everything non-urgent. So now you got your 90 non-urgent documents in the correct bucket, but you also lost the 10 urgent ones.

Same Accuracy. <i>Vastly different consequences.</i>

Wouldn’t it be great if we had some other measure to find out whether we(at the minimum) at least identified all the urgent documents? <b>OR</b> how many documents in your predicted urgent documents, were actually urgent?

Enter Recall and Precision.

For now, think of them as :

* <b><u>Recall</u></b>: <i>How many of the urgent documents in the test pool, were we able to identify correctly as urgent.</i>

* <b><u>Precision</u></b>: <i>How many of our predicted urgent documents are actually urgent. </i>

As you may have guessed from the keyword “urgent”, we cannot misclassify an urgent document. We could probably do with misclassifying a couple non-urgent documents as urgent. But absolutely no misses on urgent documents. Hence, it should be obvious that we need to optimize for Recall.

But wait! Don’t we always optimize for Recall?

<i>Not really</i>. Consider this scenario: You build a search engine, and need to return documents(<i>search results</i>) related to a search term. Do you really care to optimize your system to get every possible related page and include a whole bunch of unrelated ones in the process? Or do you care about the fact that whatever few documents your system returns as relevant, should definitely be relevant?
Exactly.

The following is called a confusion matrix. It’s simply a better way to look at how your model did and makes it easier to visualize your precision and recall.
( positives = <i>urgent documents</i> ; negatives = <i>non-urgent documents</i>)

![alt text][conf_mat]

Hence, Precision and Recall will be  :

![alt text][predrec_math]

You should now be able to relate this to our understanding of :

![alt text][predrec_doc_1]

![alt text][predrec_doc_2]

If it didn’t hit you yet, spend some time on the confusion matrix. It’ll all make sense.

The lesson to be learned here is, when using machine learning to solve problems for your business, be clear on <i><b>what performance metric defines success for you</b></i>. Is it Recall? Precision?
Or a decent mix of both?

Finally, we’re left with this big question. <i>Do we ever care about Accuracy?</i>

Sure we do. But I’ll let you figure that one out on your own 😃

<b>PS</b>: There’s all that jazz on the Precision-Recall curve and how they depend on each other and the F-score and much more. We’ll discuss them soon enough.

<i>See you in the next one!</i> 😃

[precision_recall_darts]: https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/pexels-photo-226575.jpeg "Define bulls eye"

[conf_mat]: https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/1.png "Courtesy : Matlab"

[predrec_math]: https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/pr1.png "Courtesy : Wikipedia"

[predrec_doc_1]: https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/p1.png "Courtesy : Wikipedia"

[predrec_doc_2]: https://github.com/dsouzadaniel/dsouzadaniel.github.io/raw/master/images/r1.png "Courtesy : Wikipedia"