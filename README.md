# OpenLXP-P1-Notifications

Provides an abstracted method of interacting with the mail server avaliable in Platform One.

## Installation

After running `pip install openlxp_P1_notification` add the following to the settings.py file as needed.

```python
INSTALLED_APPS = [
    ...
    'openlxp_P1_notification',
    ...
]
```

Adding `openlxp_P1_notification` to the `INSTALLED_APPS` is required for use.

```python
MIDDLEWARE = [
    ...
    'openlxp_P1_notification.middleware.TemplateMiddleware',
    ...
]
```

Add the `TemplateMiddleware` to `MIDDLEWARE` in order to load email templates.

## Django Admin

This section covers configurations that can be set in the Django Admin.

### Recipient

Recipient allows setting a name and email that should receive an email.

First_name and last_name are strings of the name the email should be addressed to.

Email_address is the unique email address the email should be sent to.

### Subject

Subject allows setting the subject line of a sent email.

Subject is the string of the subject line of the email.

### Template

Template allows tracking of `template_type`, `message`, and `template_inputs`.  Due to requirements for how emails are handled by Platform One, this should not be manually set, instead run the `load_templates` command (`python manage.py load_templates`) to load the existing templates.

### Email

Email allows for the connection of Recipient, Subject, and Template objects with a sender and reference.

Recipient, Subject, and Template should all be references to existing objects.

Sender is not used in Platform One.

Reference is an internal identifier for tracking the type of email that this configuration is for.

## Use

We provide `EmailSerializer` and `TemplateSerializer` to facilitate working with these objects within your code.

The `get-email-request/<str:request_id>` API can be used to check the status of email within the Platform One email server.

The utility `send_email` accepts the email body, along with the template type, in order to send an email.

Two sample implementations (`trigger_status_update` and `trigger_subscribed_list_update`) are defined within the management commands, and can be referenced for how to send emails.
