```python
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.naive_bayes import MultinomialNB
from sklearn.pipeline import make_pipeline
import random

tasks = pd.DataFrame(columns=['description', 'priority'])

try:
    tasks = pd.read_csv('tasks.csv')
except FileNotFoundError:
    pass


def save_tasks():
    tasks.to_csv('tasks.csv', index=False)


vectorizer = CountVectorizer()
clf = MultinomialNB()
model = make_pipeline(vectorizer, clf)
model.fit(tasks['description'], tasks['priority'])


def add_task(description, priority):
    global tasks  # Declare tasks as a global variable
    new_task = pd.DataFrame({'description': [description], 'priority': [priority]})
    tasks = pd.concat([tasks, new_task], ignore_index=True)
    save_tasks()



def remove_task(description):
    global tasks
    tasks = tasks[tasks['description'] != description]
    save_tasks()


def list_tasks():
    if tasks.empty:
        print("No tasks available.")
    else:
        print(tasks)


def recommend_task():
    if not tasks.empty:
        
        high_priority_tasks = tasks[tasks['priority'] == 'High']
        
        if not high_priority_tasks.empty:
            
            random_task = random.choice(high_priority_tasks['description'])
            print(f"Recommended task: {random_task} - Priority: High")
        else:
            print("No high-priority tasks available for recommendation.")
    else:
        print("No tasks available for recommendations.")
4

# Main menu
while True:
    print("\nTask Management App")
    print("1. Add Task")
    print("2. Remove Task")
    print("3. List Tasks")
    print("4. Recommend Task")
    print("5. Exit")

    choice = input("Select an option: ")

    if choice == "1":
        description = input("Enter task description: ")
        priority = input("Enter task priority (Low/Medium/High): ").capitalize()
        add_task(description, priority)
        print("Task added successfully.")

    elif choice == "2":
        description = input("Enter task description to remove: ")
        remove_task(description)
        print("Task removed successfully.")

    elif choice == "3":
        list_tasks()

    elif choice == "4":
        recommend_task()

    elif choice == "5":
        print("Goodbye!")
        break

    else:
        print("Invalid option. Please select a valid option.")
```

    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  1
    Enter task description:  buy groceries
    Enter task priority (Low/Medium/High):  high
    

    Task added successfully.
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  1
    Enter task description:  complete project report
    Enter task priority (Low/Medium/High):  medium
    

    Task added successfully.
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  1
    Enter task description:  schedule a meeting with the team
    Enter task priority (Low/Medium/High):  low
    

    Task added successfully.
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  1
    Enter task description:  prepare presentation for the meeting
    Enter task priority (Low/Medium/High):  medium
    

    Task added successfully.
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  1
    Enter task description:  pay the bill
    Enter task priority (Low/Medium/High):  high
    

    Task added successfully.
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  1
    Enter task description:  exercise
    Enter task priority (Low/Medium/High):  low
    

    Task added successfully.
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  2
    Enter task description to remove:  exercise
    

    Task removed successfully.
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  3
    

                                 description priority
    0                          Buy groceries     High
    1                Complete project report   Medium
    2       Schedule a meeting with the team      Low
    3   Prepare presentation for the meeting   Medium
    4                          Pay the bills     High
    5                          Buy groceries     High
    6                complete project report   Medium
    7       Schedule a meeting with the team      Low
    8   Prepare presentation for the meeting   Medium
    9                          Buy groceries     High
    10               Complete Project report   Medium
    11      Schedule a meeting with the team      Low
    12  Prepare presentation for the meeting   Medium
    13                          Pay the bill     High
    14                         buy groceries     High
    15               complete project report   Medium
    16      schedule a meeting with the team      Low
    17  prepare presentation for the meeting   Medium
    18                          pay the bill     High
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  4
    

    Recommended task: Buy groceries - Priority: High
    
    Task Management App
    1. Add Task
    2. Remove Task
    3. List Tasks
    4. Recommend Task
    5. Exit
    

    Select an option:  5
    

    Goodbye!
    


```python

```
