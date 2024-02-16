# Django Basics

**2/6/2024 • Mya Schroder**

### Views

Function-Based Views are best suited for handling simple use cases, such as a straightforward form or a page that displays static information.

Class-Based Views shine in more complex scenarios where you might benefit from the object-oriented features like inheritance. They are particularly useful for creating CRUD (Create, Read, Update, Delete) operations and when you're working with forms and models. Class views are recommended for APIs.

### DRF

DRF is a Django REST Framework library.

It's recommended to start api versioning right off the bat, so future changes don't mess up previous changes.

```py
urlpatterns = [
    path('api/v1/my_endpoint/', views.MyEndpointV1.as_view()),
    path('api/v2/my_endpoint/', views.MyEndpointV2.as_view()),
]
```

Citation: ChatGPT

### Calling REST API from Templates
Resources:

https://stackoverflow.com/questions/69640117/how-can-i-call-the-api-in-template
https://stackoverflow.com/questions/36975619/how-to-call-a-rest-web-service-api-from-javascript


### Forms
Forms are kind of like modals and serialization. Here's a good resource:

https://docs.djangoproject.com/en/5.0/topics/forms/



### Error Codes
Here's some HTTP Error Codes I used:
https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#successful_responses
