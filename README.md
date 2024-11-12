# Ex02 Django Polls
## Date: 

## AIM
To develop a Django application to implement polls.


## DESIGN STEPS

### STEP 1:
Clone the problem from GitHub

### STEP 2:
Create a new app in Django project

### STEP 3:
Enter the code for admin.py and models.py

### STEP 4:
Execute Django admin and create details for polls.

## PROGRAM
## views.py
```
from django.http import HttpResponseRedirect, HttpResponse
from django.shortcuts import get_object_or_404, render
from django.urls import reverse
from django.views import generic

from .models import Choice, Question

class IndexView(generic.ListView):
    template_name = "polls/index.html"
    context_object_name = "latest_question_list"

    def get_queryset(self):
        """Return the last five published questions."""
        return Question.objects.order_by("-pub_date")[:5]


class DetailView(generic.DetailView):
    model = Question
    template_name = "polls/detail.html"


class ResultsView(generic.DetailView):
    model = Question
    template_name = "polls/results.html"

def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST["choice"])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(
            request,
            "polls/detail.html",
            {
                "question": question,
                "error_message": "You didn't select a choice.",
            },
        )
    else:
        selected_choice.votes += 1
        selected_choice.save()
        # Always return an HttpResponseRedirect after successfully dealing
        # with POST data. This prevents data from being posted twice if a
        # user hits the Back button.
        return HttpResponseRedirect(reverse("polls:results", args=(question.id,)))

def owner(request):
        return HttpResponse("Hello, world. e8f7c605 is the polls owner.")
def owner(request):
        return HttpResponse("Hello, world. 11f2a99d is the polls owner.")
```

## urls.py
```
from django.urls import path

from . import views

app_name = "polls"

urlpatterns = [
    path('', views.IndexView.as_view(), name='index'),
    path('owner', views.owner, name='owner'),
    path('<int:pk>/', views.DetailView.as_view(), name='detail'),
    path('<int:pk>/results/', views.ResultsView.as_view(), name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```


## OUTPUT
![image](https://github.com/user-attachments/assets/6cc27102-41e9-4ccc-b1f9-20ba07c56a2e)
![image](https://github.com/user-attachments/assets/47989bca-a5ac-442d-8e97-7dbc6197e3df)
![image](https://github.com/user-attachments/assets/bb51b3c8-3613-4fc6-8f85-33ce1eb7607a)


## COURSERA GRADE
![image](https://github.com/user-attachments/assets/c4e8afc4-5893-4e75-aa61-6e6d84770b51)

## RESULT
Thus the program for creating a polls using Django has been executed successfully.
