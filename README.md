```
cd hello-airflow
export AIRFLOW_HOME=/Users/HashNuke/projects/hello-airflow/airflow
mkdir -p airflow/dags
airflow initdb
```

```
$ ls airflow
airflow.cfg   airflow.db    dags          unittests.cfg
```

Create `airflow/dags/hello.py` from <http://pythonhosted.org/airflow/tutorial.html>




```
$ python airflow/dags/hello.py
[2017-07-19 01:10:54,022] {__init__.py:57} INFO - Using executor SequentialExecutor
```


```
$ airflow list_dags
airflow list_dags
[2017-07-19 01:12:00,591] {__init__.py:57} INFO - Using executor SequentialExecutor
[2017-07-19 01:12:00,997] {models.py:168} INFO - Filling up the DagBag from /Users/HashNuke/projects/hello-airflow/airflow/dags


-------------------------------------------------------------------
DAGS
-------------------------------------------------------------------
example_bash_operator
example_branch_dop_operator_v3
example_branch_operator
example_http_operator
example_passing_params_via_test_command
example_python_operator
example_short_circuit_operator
example_skip_dag
example_subdag_operator
example_subdag_operator.section-1
example_subdag_operator.section-2
example_trigger_controller_dag
example_trigger_target_dag
example_xcom
hello
latest_only
latest_only_with_trigger
test_utils
tutorial
```

```
$ airflow list_tasks hello
[2017-07-19 01:12:55,474] {__init__.py:57} INFO - Using executor SequentialExecutor
[2017-07-19 01:12:55,874] {models.py:168} INFO - Filling up the DagBag from /Users/HashNuke/projects/hello-airflow/airflow/dags
print_date
sleep
templated
```

```
$ airflow list_tasks hello --tree
[2017-07-19 01:13:11,689] {__init__.py:57} INFO - Using executor SequentialExecutor
[2017-07-19 01:13:12,088] {models.py:168} INFO - Filling up the DagBag from /Users/HashNuke/projects/hello-airflow/airflow/dags
<Task(BashOperator): sleep>
    <Task(BashOperator): print_date>
<Task(BashOperator): templated>
    <Task(BashOperator): print_date>
```

```
$ airflow test hello print_date 2015-06-01
[2017-07-19 01:13:26,749] {__init__.py:57} INFO - Using executor SequentialExecutor
[2017-07-19 01:13:27,148] {models.py:168} INFO - Filling up the DagBag from /Users/HashNuke/projects/hello-airflow/airflow/dags
/Users/HashNuke/.local/share/virtualenvs/hello-airflow-dxWcFd6V/lib/python3.6/site-packages/airflow/models.py:1142: DeprecationWarning: generator 'get_dep_statuses' raised StopIteration
  dep_context):
/Users/HashNuke/.local/share/virtualenvs/hello-airflow-dxWcFd6V/lib/python3.6/site-packages/airflow/ti_deps/deps/base_ti_dep.py:100: DeprecationWarning: generator '_get_dep_statuses' raised StopIteration
  for dep_status in self._get_dep_statuses(ti, session, dep_context):
[2017-07-19 01:13:28,049] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-01 00:00:00 [None]>
[2017-07-19 01:13:28,052] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-01 00:00:00 [None]>
[2017-07-19 01:13:28,052] {models.py:1328} INFO -
--------------------------------------------------------------------------------
Starting attempt 1 of 2
--------------------------------------------------------------------------------

[2017-07-19 01:13:28,052] {models.py:1352} INFO - Executing <Task(BashOperator): print_date> on 2015-06-01 00:00:00
[2017-07-19 01:13:28,071] {bash_operator.py:71} INFO - tmp dir root location:
/var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T
[2017-07-19 01:13:28,072] {bash_operator.py:80} INFO - Temporary script location :/var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T/airflowtmpyvecmw9u//var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T/airflowtmpyvecmw9u/print_daten_zyzzvg
[2017-07-19 01:13:28,073] {bash_operator.py:81} INFO - Running command: date
[2017-07-19 01:13:28,078] {bash_operator.py:90} INFO - Output:
[2017-07-19 01:13:28,086] {bash_operator.py:94} INFO - Wed Jul 19 01:13:28 IST 2017
[2017-07-19 01:13:28,087] {bash_operator.py:97} INFO - Command exited with return code 0
```

```
$ airflow test hello sleep 2015-06-01
[2017-07-19 01:13:50,700] {__init__.py:57} INFO - Using executor SequentialExecutor
[2017-07-19 01:13:51,118] {models.py:168} INFO - Filling up the DagBag from /Users/HashNuke/projects/hello-airflow/airflow/dags
/Users/HashNuke/.local/share/virtualenvs/hello-airflow-dxWcFd6V/lib/python3.6/site-packages/airflow/models.py:1142: DeprecationWarning: generator 'get_dep_statuses' raised StopIteration
  dep_context):
/Users/HashNuke/.local/share/virtualenvs/hello-airflow-dxWcFd6V/lib/python3.6/site-packages/airflow/ti_deps/deps/base_ti_dep.py:100: DeprecationWarning: generator '_get_dep_statuses' raised StopIteration
  for dep_status in self._get_dep_statuses(ti, session, dep_context):
[2017-07-19 01:13:51,632] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-01 00:00:00 [None]>
[2017-07-19 01:13:51,635] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-01 00:00:00 [None]>
[2017-07-19 01:13:51,635] {models.py:1328} INFO -
--------------------------------------------------------------------------------
Starting attempt 1 of 4
--------------------------------------------------------------------------------

[2017-07-19 01:13:51,635] {models.py:1352} INFO - Executing <Task(BashOperator): sleep> on 2015-06-01 00:00:00
[2017-07-19 01:13:51,656] {bash_operator.py:71} INFO - tmp dir root location:
/var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T
[2017-07-19 01:13:51,658] {bash_operator.py:80} INFO - Temporary script location :/var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T/airflowtmp17s0qdzn//var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T/airflowtmp17s0qdzn/sleep9isu_vi0
[2017-07-19 01:13:51,658] {bash_operator.py:81} INFO - Running command: sleep 5
[2017-07-19 01:13:51,664] {bash_operator.py:90} INFO - Output:
[2017-07-19 01:13:56,673] {bash_operator.py:97} INFO - Command exited with return code 0
```

```
$ airflow test hello templated 2015-06-01
[2017-07-19 01:14:15,966] {__init__.py:57} INFO - Using executor SequentialExecutor
[2017-07-19 01:14:16,362] {models.py:168} INFO - Filling up the DagBag from /Users/HashNuke/projects/hello-airflow/airflow/dags
/Users/HashNuke/.local/share/virtualenvs/hello-airflow-dxWcFd6V/lib/python3.6/site-packages/airflow/ti_deps/deps/base_ti_dep.py:100: DeprecationWarning: generator '_get_dep_statuses' raised StopIteration
  for dep_status in self._get_dep_statuses(ti, session, dep_context):
/Users/HashNuke/.local/share/virtualenvs/hello-airflow-dxWcFd6V/lib/python3.6/site-packages/airflow/models.py:1142: DeprecationWarning: generator 'get_dep_statuses' raised StopIteration
  dep_context):
[2017-07-19 01:14:16,838] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-01 00:00:00 [None]>
[2017-07-19 01:14:16,841] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-01 00:00:00 [None]>
[2017-07-19 01:14:16,841] {models.py:1328} INFO -
--------------------------------------------------------------------------------
Starting attempt 1 of 2
--------------------------------------------------------------------------------

[2017-07-19 01:14:16,841] {models.py:1352} INFO - Executing <Task(BashOperator): templated> on 2015-06-01 00:00:00
[2017-07-19 01:14:16,864] {bash_operator.py:71} INFO - tmp dir root location:
/var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T
[2017-07-19 01:14:16,865] {bash_operator.py:80} INFO - Temporary script location :/var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T/airflowtmpe_30viak//var/folders/gt/80qfljmx3f94ndtbcjfnf3hr0000gn/T/airflowtmpe_30viak/templatede5soy6n7
[2017-07-19 01:14:16,866] {bash_operator.py:81} INFO - Running command:

        echo "2015-06-01"
        echo "2015-06-08"
        echo "Parameter I passed in"

        echo "2015-06-01"
        echo "2015-06-08"
        echo "Parameter I passed in"

        echo "2015-06-01"
        echo "2015-06-08"
        echo "Parameter I passed in"

        echo "2015-06-01"
        echo "2015-06-08"
        echo "Parameter I passed in"

        echo "2015-06-01"
        echo "2015-06-08"
        echo "Parameter I passed in"

[2017-07-19 01:14:16,871] {bash_operator.py:90} INFO - Output:
[2017-07-19 01:14:16,874] {bash_operator.py:94} INFO - 2015-06-01
[2017-07-19 01:14:16,874] {bash_operator.py:94} INFO - 2015-06-08
[2017-07-19 01:14:16,874] {bash_operator.py:94} INFO - Parameter I passed in
[2017-07-19 01:14:16,874] {bash_operator.py:94} INFO - 2015-06-01
[2017-07-19 01:14:16,874] {bash_operator.py:94} INFO - 2015-06-08
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - Parameter I passed in
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - 2015-06-01
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - 2015-06-08
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - Parameter I passed in
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - 2015-06-01
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - 2015-06-08
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - Parameter I passed in
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - 2015-06-01
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - 2015-06-08
[2017-07-19 01:14:16,875] {bash_operator.py:94} INFO - Parameter I passed in
[2017-07-19 01:14:16,876] {bash_operator.py:97} INFO - Command exited with return code 0
```

```
$ airflow backfill hello -s 2015-06-01 -e 2015-06-07
[2017-07-19 01:14:58,479] {__init__.py:57} INFO - Using executor SequentialExecutor
[2017-07-19 01:14:58,886] {models.py:168} INFO - Filling up the DagBag from /Users/HashNuke/projects/hello-airflow/airflow/dags
/Users/HashNuke/.local/share/virtualenvs/hello-airflow-dxWcFd6V/lib/python3.6/site-packages/airflow/ti_deps/deps/base_ti_dep.py:100: DeprecationWarning: generator '_get_dep_statuses' raised StopIteration
  for dep_status in self._get_dep_statuses(ti, session, dep_context):
[2017-07-19 01:14:59,788] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-01 00:00:00 [scheduled]>
[2017-07-19 01:14:59,793] {base_executor.py:50} INFO - Adding to queue: airflow run hello print_date 2015-06-01T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:14:59,802] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-02 00:00:00 [scheduled]>
[2017-07-19 01:14:59,806] {base_executor.py:50} INFO - Adding to queue: airflow run hello print_date 2015-06-02T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:14:59,816] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-03 00:00:00 [scheduled]>
[2017-07-19 01:14:59,820] {base_executor.py:50} INFO - Adding to queue: airflow run hello print_date 2015-06-03T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:14:59,831] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-04 00:00:00 [scheduled]>
[2017-07-19 01:14:59,835] {base_executor.py:50} INFO - Adding to queue: airflow run hello print_date 2015-06-04T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:14:59,844] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-05 00:00:00 [scheduled]>
[2017-07-19 01:14:59,848] {base_executor.py:50} INFO - Adding to queue: airflow run hello print_date 2015-06-05T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:14:59,857] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-06 00:00:00 [scheduled]>
[2017-07-19 01:14:59,863] {base_executor.py:50} INFO - Adding to queue: airflow run hello print_date 2015-06-06T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:14:59,871] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.print_date 2015-06-07 00:00:00 [scheduled]>
[2017-07-19 01:14:59,877] {base_executor.py:50} INFO - Adding to queue: airflow run hello print_date 2015-06-07T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:14:59,893] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.sleep 2015-06-01 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,901] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.sleep 2015-06-02 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,909] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.sleep 2015-06-03 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,919] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.sleep 2015-06-04 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,932] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.sleep 2015-06-05 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,942] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.sleep 2015-06-06 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,952] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.sleep 2015-06-07 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,961] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.templated 2015-06-01 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,971] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.templated 2015-06-02 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,983] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.templated 2015-06-03 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,991] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.templated 2015-06-04 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:14:59,999] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.templated 2015-06-05 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:15:00,008] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.templated 2015-06-06 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:15:00,019] {models.py:1122} INFO - Dependencies not met for <TaskInstance: hello.templated 2015-06-07 00:00:00 [scheduled]>, dependency 'Trigger Rule' FAILED: Task's trigger rule 'all_success' requires all upstream tasks to have succeeded, but found 1 non-success(es). upstream_tasks_state={'successes': 0, 'skipped': 0, 'failed': 0, 'upstream_failed': 0, 'done': 0}, upstream_task_ids=['print_date']
[2017-07-19 01:15:04,418] {sequential_executor.py:40} INFO - Executing command: airflow run hello print_date 2015-06-01T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:04,766] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/print_date/2015-06-01T00:00:00
[2017-07-19 01:15:10,828] {sequential_executor.py:40} INFO - Executing command: airflow run hello print_date 2015-06-02T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:11,378] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/print_date/2015-06-02T00:00:00
[2017-07-19 01:15:17,810] {sequential_executor.py:40} INFO - Executing command: airflow run hello print_date 2015-06-03T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:18,253] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/print_date/2015-06-03T00:00:00
[2017-07-19 01:15:24,718] {sequential_executor.py:40} INFO - Executing command: airflow run hello print_date 2015-06-04T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:25,059] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/print_date/2015-06-04T00:00:00
[2017-07-19 01:15:31,108] {sequential_executor.py:40} INFO - Executing command: airflow run hello print_date 2015-06-05T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:31,449] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/print_date/2015-06-05T00:00:00
[2017-07-19 01:15:37,462] {sequential_executor.py:40} INFO - Executing command: airflow run hello print_date 2015-06-06T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:37,788] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/print_date/2015-06-06T00:00:00
[2017-07-19 01:15:43,782] {sequential_executor.py:40} INFO - Executing command: airflow run hello print_date 2015-06-07T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:44,094] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/print_date/2015-06-07T00:00:00
[2017-07-19 01:15:50,110] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-01 00:00:00: backfill_2015-06-01T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:15:50,128] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-02 00:00:00: backfill_2015-06-02T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:15:50,138] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-03 00:00:00: backfill_2015-06-03T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:15:50,155] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-04 00:00:00: backfill_2015-06-04T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:15:50,169] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-05 00:00:00: backfill_2015-06-05T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:15:50,186] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-06 00:00:00: backfill_2015-06-06T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:15:50,198] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-07 00:00:00: backfill_2015-06-07T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:15:50,206] {jobs.py:2002} INFO - [backfill progress] | finished run 0 of 7 | tasks waiting: 14 | succeeded: 7 | kicked_off: 0 | failed: 0 | skipped: 0 | deadlocked: 0 | not ready: 14
[2017-07-19 01:15:50,216] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-01 00:00:00 [scheduled]>
[2017-07-19 01:15:50,220] {base_executor.py:50} INFO - Adding to queue: airflow run hello sleep 2015-06-01T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,239] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-02 00:00:00 [scheduled]>
[2017-07-19 01:15:50,243] {base_executor.py:50} INFO - Adding to queue: airflow run hello sleep 2015-06-02T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,256] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-03 00:00:00 [scheduled]>
[2017-07-19 01:15:50,259] {base_executor.py:50} INFO - Adding to queue: airflow run hello sleep 2015-06-03T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,273] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-04 00:00:00 [scheduled]>
[2017-07-19 01:15:50,278] {base_executor.py:50} INFO - Adding to queue: airflow run hello sleep 2015-06-04T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,296] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-05 00:00:00 [scheduled]>
[2017-07-19 01:15:50,299] {base_executor.py:50} INFO - Adding to queue: airflow run hello sleep 2015-06-05T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,311] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-06 00:00:00 [scheduled]>
[2017-07-19 01:15:50,315] {base_executor.py:50} INFO - Adding to queue: airflow run hello sleep 2015-06-06T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,330] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.sleep 2015-06-07 00:00:00 [scheduled]>
[2017-07-19 01:15:50,339] {base_executor.py:50} INFO - Adding to queue: airflow run hello sleep 2015-06-07T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,352] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-01 00:00:00 [scheduled]>
[2017-07-19 01:15:50,355] {base_executor.py:50} INFO - Adding to queue: airflow run hello templated 2015-06-01T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,370] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-02 00:00:00 [scheduled]>
[2017-07-19 01:15:50,374] {base_executor.py:50} INFO - Adding to queue: airflow run hello templated 2015-06-02T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,393] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-03 00:00:00 [scheduled]>
[2017-07-19 01:15:50,396] {base_executor.py:50} INFO - Adding to queue: airflow run hello templated 2015-06-03T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,407] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-04 00:00:00 [scheduled]>
[2017-07-19 01:15:50,411] {base_executor.py:50} INFO - Adding to queue: airflow run hello templated 2015-06-04T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,425] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-05 00:00:00 [scheduled]>
[2017-07-19 01:15:50,431] {base_executor.py:50} INFO - Adding to queue: airflow run hello templated 2015-06-05T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,448] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-06 00:00:00 [scheduled]>
[2017-07-19 01:15:50,451] {base_executor.py:50} INFO - Adding to queue: airflow run hello templated 2015-06-06T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,465] {models.py:1128} INFO - Dependencies all met for <TaskInstance: hello.templated 2015-06-07 00:00:00 [scheduled]>
[2017-07-19 01:15:50,469] {base_executor.py:50} INFO - Adding to queue: airflow run hello templated 2015-06-07T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,561] {sequential_executor.py:40} INFO - Executing command: airflow run hello sleep 2015-06-01T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:15:50,905] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/sleep/2015-06-01T00:00:00
[2017-07-19 01:16:01,927] {sequential_executor.py:40} INFO - Executing command: airflow run hello sleep 2015-06-02T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:16:02,251] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/sleep/2015-06-02T00:00:00
[2017-07-19 01:16:13,280] {sequential_executor.py:40} INFO - Executing command: airflow run hello sleep 2015-06-03T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:16:13,596] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/sleep/2015-06-03T00:00:00
[2017-07-19 01:16:24,664] {sequential_executor.py:40} INFO - Executing command: airflow run hello sleep 2015-06-04T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:16:25,027] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/sleep/2015-06-04T00:00:00
[2017-07-19 01:16:36,048] {sequential_executor.py:40} INFO - Executing command: airflow run hello sleep 2015-06-05T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:16:36,377] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/sleep/2015-06-05T00:00:00
[2017-07-19 01:16:47,407] {sequential_executor.py:40} INFO - Executing command: airflow run hello sleep 2015-06-06T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:16:47,743] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/sleep/2015-06-06T00:00:00
[2017-07-19 01:16:58,966] {sequential_executor.py:40} INFO - Executing command: airflow run hello sleep 2015-06-07T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:16:59,303] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/sleep/2015-06-07T00:00:00
[2017-07-19 01:17:10,416] {sequential_executor.py:40} INFO - Executing command: airflow run hello templated 2015-06-01T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:17:10,861] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/templated/2015-06-01T00:00:00
[2017-07-19 01:17:16,974] {sequential_executor.py:40} INFO - Executing command: airflow run hello templated 2015-06-02T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:17:17,306] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/templated/2015-06-02T00:00:00
[2017-07-19 01:17:23,382] {sequential_executor.py:40} INFO - Executing command: airflow run hello templated 2015-06-03T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:17:23,710] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/templated/2015-06-03T00:00:00
[2017-07-19 01:17:29,757] {sequential_executor.py:40} INFO - Executing command: airflow run hello templated 2015-06-04T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:17:30,103] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/templated/2015-06-04T00:00:00
[2017-07-19 01:17:36,420] {sequential_executor.py:40} INFO - Executing command: airflow run hello templated 2015-06-05T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:17:36,768] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/templated/2015-06-05T00:00:00
[2017-07-19 01:17:42,803] {sequential_executor.py:40} INFO - Executing command: airflow run hello templated 2015-06-06T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:17:43,130] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/templated/2015-06-06T00:00:00
[2017-07-19 01:17:49,159] {sequential_executor.py:40} INFO - Executing command: airflow run hello templated 2015-06-07T00:00:00 --local -sd DAGS_FOLDER/hello.py
[2017-07-19 01:17:49,492] {__init__.py:57} INFO - Using executor SequentialExecutor
Logging into: /Users/HashNuke/projects/hello-airflow/airflow/logs/hello/templated/2015-06-07T00:00:00
[2017-07-19 01:17:55,623] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-01 00:00:00: backfill_2015-06-01T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:17:55,626] {models.py:4178} INFO - Marking run <DagRun hello @ 2015-06-01 00:00:00: backfill_2015-06-01T00:00:00, externally triggered: False> successful
[2017-07-19 01:17:55,637] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-02 00:00:00: backfill_2015-06-02T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:17:55,639] {models.py:4178} INFO - Marking run <DagRun hello @ 2015-06-02 00:00:00: backfill_2015-06-02T00:00:00, externally triggered: False> successful
[2017-07-19 01:17:55,653] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-03 00:00:00: backfill_2015-06-03T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:17:55,656] {models.py:4178} INFO - Marking run <DagRun hello @ 2015-06-03 00:00:00: backfill_2015-06-03T00:00:00, externally triggered: False> successful
[2017-07-19 01:17:55,674] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-04 00:00:00: backfill_2015-06-04T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:17:55,677] {models.py:4178} INFO - Marking run <DagRun hello @ 2015-06-04 00:00:00: backfill_2015-06-04T00:00:00, externally triggered: False> successful
[2017-07-19 01:17:55,688] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-05 00:00:00: backfill_2015-06-05T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:17:55,690] {models.py:4178} INFO - Marking run <DagRun hello @ 2015-06-05 00:00:00: backfill_2015-06-05T00:00:00, externally triggered: False> successful
[2017-07-19 01:17:55,707] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-06 00:00:00: backfill_2015-06-06T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:17:55,713] {models.py:4178} INFO - Marking run <DagRun hello @ 2015-06-06 00:00:00: backfill_2015-06-06T00:00:00, externally triggered: False> successful
[2017-07-19 01:17:55,725] {models.py:4132} INFO - Updating state for <DagRun hello @ 2015-06-07 00:00:00: backfill_2015-06-07T00:00:00, externally triggered: False> considering 3 task(s)
[2017-07-19 01:17:55,727] {models.py:4178} INFO - Marking run <DagRun hello @ 2015-06-07 00:00:00: backfill_2015-06-07T00:00:00, externally triggered: False> successful
[2017-07-19 01:17:55,737] {jobs.py:2002} INFO - [backfill progress] | finished run 7 of 7 | tasks waiting: 0 | succeeded: 21 | kicked_off: 0 | failed: 0 | skipped: 0 | deadlocked: 0 | not ready: 0
[2017-07-19 01:17:55,738] {jobs.py:2047} INFO - Backfill done. Exiting.
```