# Django and AngularJS template tags conflict

Django and AngularJS share the same token for variable substitution in templates, ie. double curly braces. 

__This should not be a big problem, since you are discouraged to mix Django template code with AngularJS template code.__

The cleanest solution to circumvent this, is by using the [[https://docs.djangoproject.com/en/1.10/ref/templates/builtins/#verbatim|verbatim]] tag, which became available in Django 1.5.

<file>
{% verbatim %}
    {{if dying}}Still alive.{{/if}}
{% endverbatim %}
</file>

You can also designate a specific closing tag, allowing the use of {% endverbatim %} as part of the unrendered contents:

<file>
{% verbatim myblock %}
    Avoid template rendering via the {% verbatim %}{% endverbatim %} block.
{% endverbatim myblock %}
</file>