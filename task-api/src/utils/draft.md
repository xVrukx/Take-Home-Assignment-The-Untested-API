## fetures already have

GET	/tasks	List all tasks. Supports ?status=, ?page=,(
    on path status, page, limit: 200 response
    )

<!-- ----------------------------------------------------------- -->

POST	/tasks	Create a new (    
    on path task with body attribute contaning invalid data: {
        "error": "status must be one of: todo, in_progress, done","duedate, created date, must not be null"
        }

instead of this

  "status": "pending | in-progress | completed",

)

<!-- ----------------------------------------------------------- -->

GET	/tasks/stats	Counts by status + overdue count (
    works correctly
)

## problem

POST	/tasks	Create a new (    
    on path task with body attribute contaning invalid data: {
        "problem": "duedate accept any number if not null, created at and completeted can be updated and accept any alpha numric value"
        }
)

<!-- ----------------------------------------------------------- -->

?limit=(
      limit is not working
)

PUT	/tasks/:id	Update a task can update id, duedate accept any number if not null, created at and completeted can be updated and accept any alpha numric value statu can be changed to done(complete and priority doesnt changes, no sence of having task/:id/complete if update can change it)"