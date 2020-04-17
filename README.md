README
======

"Operation Manhattan" contains Org files for managing reading time.

This project is inspired from [mbuf's Operation Blue Moon][obm].

[obm]: https://gitlab.com/shakthimaan/operation-blue-moon/

Motivation
==========

* Reading more
* Time management
* Better estimation
* Self-improvement
* Statistics

Workflow
========

If you are interested in participating in these sprints, list down the
books you want to read (in next 1 year), and email rj722 [at] protonmail [dot] com.

### What?

Create an Org file in `plan/` directory with your GitHub username. See
`plan/user-example.org` reference.

For every book you want to read, create a task into `plan/<USERNAME.org>`. Under
this heading, create a checklist with all the chapters of the book (along with
time estimates).

You can insert a new task into your plan file by invoking `M-x
insert-org-manhattan-entry` after adding the following function to your Emacs
init configuration:

(NOTE: For spacemacs related config, [see this gist][gist])

[gist]: https://gist.github.com/RJ722/5a411efc7c99c34083c77ddc757168bf

```lisp
(define-skeleton insert-org-manhattan-entry
  "Prompt for task, estimate and category"
  nil
  '(setq task  (skeleton-read "Task: "))
  '(setq estimate  (skeleton-read "Estimate: "))
  '(setq timestamp (format-time-string "%s"))
  "** TODO " task \n
  ":PROPERTIES:" \n
  ":ESTIMATED: " estimate \n
  ":ACTUAL:" \n
  ":OWNER: <YOUR_USERNAME_HERE>" \n
  ":ID: READ." timestamp \n
  ":TASKID: READ." timestamp \n
  ":END:")
```

A task that spans across multiple sprints should have the same ID and
TASKID, but, you can add a suffix to the task name as "Part I", "Part
II", "Part III" etc. across sprints. This helps to track the total
time spent on a task.

### When?

For each sprint, you list the tasks that you want to work under the
PLAN heading in your Org file.

You should also decide on the hours you can spend per day and create a
work-per-day entry for each sprint in the PROPERTIES drawer as shown
below:

```
** April   20, 2020 - April   29, 2020 (9 days)
    :PROPERTIES:
    :wpd-RJ722: 2
    :END:
```

You should not clock anything in your Org file. All clocked timings
will be in sprints/.

### How?

During the sprint, you can send PR with your clocked timings. You need
to ensure that ACTUALS in the PROPERTIES drawer get updated. You can
add the following to your Emacs configuration:

```lisp
(defun org-update-actuals ()
  (interactive)
  (org-entry-put (point) "ACTUAL"
                  (format "%0.2f" (/ (org-clock-sum-current-item) 60.0))))

(global-set-key (kbd "C-c s c") 'org-update-actuals)
```

At the end of a sprint, a retrospection meeting will be held to review
the same.

It is recommended for participants to wear a heavy watch so that they
have the notion of time.

Upcoming Sprints
================

* April     18, 2020 - April     30, 2020 (13 days)
* May       01, 2020 - May       16, 2020 (16 days)
* May       17, 2020 - May       29, 2020 (13 days)
* May       30, 2020 - June      16, 2020 (17 days)
* June      17, 2020 - June      30, 2020 (14 days)
* July       1, 2020 - July      16, 2020 (16 days)
* July      17, 2020 - August     2, 2020 (16 days)
* August     3, 2020 - August    18, 2020 (16 days)
* August    19, 2020 - September  2, 2020 (14 days)

Contact
=======

Rahul Jha ("RJ722")

rj722 [at] protonmail [dot] com
