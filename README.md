# Rated reviews application for Django

[![Build Status](https://travis-ci.com/andreynovikov/django-rated-reviews.svg?branch=master)](https://travis-ci.com/andreynovikov/django-rated-reviews)
[![GitHub release](https://img.shields.io/github/release/andreynovikov/django-rated-reviews.svg)](https://github.com/andreynovikov/django-rated-reviews/releases/latest)
[![PyPI release](https://img.shields.io/pypi/v/django-rated-reviews.svg)](https://pypi.org/project/django-rated-reviews/)
[![Python version](https://img.shields.io/pypi/pyversions/django-rated-reviews.svg)](https://pypi.org/project/django-rated-reviews/)
[![GitHub issues](https://img.shields.io/github/issues/andreynovikov/django-rated-reviews.svg)](https://github.com/andreynovikov/django-rated-reviews/issues)
[![Code quality](https://img.shields.io/codacy/grade/fe2c36bbb12344318d0523148ae8e725.svg)](https://www.codacy.com/app/novikov/django-rated-reviews)
[![Coverage](https://img.shields.io/codacy/coverage/fe2c36bbb12344318d0523148ae8e725.svg)](https://www.codacy.com/app/novikov/django-rated-reviews)
[![GitHub license](https://img.shields.io/github/license/andreynovikov/django-rated-reviews.svg)](LICENSE)

Rated reviews is derived from [Django “excontrib” Comments](https://github.com/django/django-contrib-comments/) and can be used to attach reviews with rating to any model. The core difference from comments is that user can provide only one review per item. Rating is expressed by a number and by default visualized with stars. However, it can be changed to whatever you want. Rating grades are also configurable.

Optionally rating can be weighted. For instance, you can designate experts whose rating would be more valuable. Alternatively, add weight to reviews of real byers of sold product.

## Requirements

* Python 2.7+ or Python 3.3+
* Django 1.11+

## Installation

Install ```django-rated-reviews``` using pip:

```shell
pip install django-rated-reviews
```

Add ```reviews``` to ```INSTALLED_APPS```. Example:

```python
INSTALLED_APPS = (
    ...
    'reviews',
    ...
)
```

Run ```manage.py migrate``` so that Django will create the review tables.

Add the reviews app’s URLs to your project’s urls.py:

```python
urlpatterns = [
    ...
    url(r'^reviews/', include('reviews.urls')),
    ...
]
```

Use the review template tags to embed reviews in your templates.

## Customization

All configuration settings are optional.

### REVIEW_MAX_LENGTH

The maximum length of the review comment field, in characters. Comments longer than this will be rejected. Defaults to ```3000```.

### REVIEW_PUBLISH_UNMODERATED

If ```False``` (default) reviews are not published until they are moderated in admin. If user modifies existing review it is considered unmoderated again.

### REVIEW_COMPOSE_TIMEOUT

The maximum review form timeout in seconds. The default value is ```2 * 60 * 60``` (2 hours).

### REVIEW_RATING_CHOICES

Custom rating choices, each represented by one star (currently the maximum supported number is 10). Default choices are:

```python
REVIEW_RATING_CHOICES = (
    ('1', _('Terrible')),
    ('2', _('Poor')),
    ('3', _('Average')),
    ('4', _('Very Good')),
    ('5', _('Excellent')),
)
```

### REVIEW_SHOW_RATING_TEXT

If ```True``` (default) rating text (as specified by choices) is displayed next to rating stars. 

### REVIEW_ALLOW_PROFANITIES

If ```False``` review comment is checked against words in ```PROFANITIES_LIST```. If it contains any of the words, review is rejected.

### REVIEW_APP

Custom reviews app can be set that will define custom ```ReviewForm```, ```Review``` model or rating weight system.

## Credits

Application code is derived from [Django “excontrib” Comments](https://github.com/django/django-contrib-comments/).

Rating widget uses [star-rating.js library](https://github.com/pryley/star-rating.js) by Paul Ryley.
