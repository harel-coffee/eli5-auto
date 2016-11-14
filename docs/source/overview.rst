Overview
========

Installation
------------

ELI5 works in Python 2.7 and Python 3.4+. Currently it requires
scikit-learn 0.18+, so make sure scikit-learn is installed first,
then install eli5 using pip::

    pip install 'scikit-learn > 0.18'
    pip install eli5

Features
--------

ELI5_ is a Python package which helps to debug machine learning
classifiers and explain their predictions. It provides support for the
following machine learning frameworks and packages:

* scikit-learn_. Currently ELI5 allows to explain weights and predictions
  of scikit-learn linear classifiers and regressors, print decision trees
  as text or as SVG, show feature importances of random forests. ELI5
  understands text processing utilities from scikit-learn and can highlight
  text data accordingly. It also allows to debug scikit-learn pipelines which
  contain HashingVectorizer, by undoing hashing.

* lightning_ - explain weights and predictions of lightning classifiers and
  regressors.

* sklearn-crfsuite_. ELI5 allows to check weights of sklearn_crfsuite.CRF
  models.

ELI5 also provides an alternative implementation of LIME_ algorithm,
which allows to explain predictions of any black-box classifier. This feature
is currently experimental.

Explanation and formatting are separated; you can get text-based explanation
to display in console, HTML version embeddable in an IPython notebook
or web dashboards, or JSON version which allows to implement custom
rendering and formatting on a client.

.. _lightning: https://github.com/scikit-learn-contrib/lightning
.. _scikit-learn: https://github.com/scikit-learn/scikit-learn
.. _sklearn-crfsuite: https://github.com/TeamHG-Memex/sklearn-crfsuite
.. _LIME: http://arxiv.org/abs/1602.04938
.. _ELI5: https://github.com/TeamHG-Memex/eli5

Basic Usage
-----------

There are two main ways to look at a classification or a regression model:

1. inspect model parameters and try to figure out how the model works
   globally;
2. inspect an individual prediction of a model, try to figure out why
   the model makes the decision it makes.

For (1) ELI5 provides ``eli5.explain_weights`` function; for (2) it provides
``eli5.explain_prediction`` function.

If the ML library you're working with is supported then you usually
can enter the following in IPython Notebook::

    import eli5
    eli5.explain_weights(clf)

and get an explanation like this:

.. image:: static/weights.png

Supported arguments and the exact way the classifier is visualized depends
on a library.

To explain an individual prediction (2) use ``eli5.explain_prediction``
function. Exact parameters depend on a classifier and on input data kind
(text, tabular, images). For example, you may get text highlighted like this
if you're using one of the scikit-learn_ vectorizers with char ngrams:

.. image:: static/char-ngrams.png


Why?
----

For some of classifiers inspection and debugging is easy, for others
this is hard. It is not a rocket science to take coefficients
of a linear classifier, relate them to feature names and show in
an HTML table. ELI5 aims to handle not only simple cases,
but even for simple cases having unified API for inspection has a value:

* you can call a ready-made function from ELI5 and get a nicely formatted
  result immediately;
* formatting code can be reused between machine learning frameworks;
* 'drill down' code like feature filtering or text highlighting can be reused;
* there are lots of gotchas and small differences which ELI5 takes care of;
* algorithms like LIME_ try to explain a black-box classifier
  through a locally-fit simple, interpretable classifier. It means that
  with each additional supported "simple" classifier/regressor
  algorithms like LIME are getting more options automatically.