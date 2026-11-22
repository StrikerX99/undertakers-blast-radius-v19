# Undertakers Blast Radius V19

Put the contents of this directory at the root of the team's public submission repository. Build with `docker build --platform linux/amd64 -t undertakers-v19 .`. The image reads the mounted commit patches and test catalog and writes one worker plan per patch.

The selector starts with test dependencies measured on SQLGlot at `eb11aec4be8cb2122afe713a4816662c3f0fb2fa`. It applies each incoming patch to an isolated checkout. Its worker allocator compares the longest worker load plus the setup cost for each feasible worker count. Unresolved cases retain their candidates. The final allocation also compares its cost with the allocation before additional checks.

The SQL workload index records inputs and generated commands at the point where SQLGlot turns a query into executable Python. The selector can compare parser outputs, optimizer results and backend SQL on the actual patch. When an individual query differs at an intermediate stage, it can execute that query against the original tables and check the test's expected result. Time limits and unsupported changes preserve the existing schedule.

The assertion index records 1,291 passing unittest methods and separately indexes 2,432 independent SQL assertions. Body edits are compared with the functions each case reached. Eligible class settings use dialect ownership and imports. The program replays affected assertions on the patch. Additional whole-test verification uses native timings measured on the pin. A batch-wide CPU allowance increases when verification cuts the simulated worker cost.

For SQL expressions built during module or class initialization, the selector links the functions that constructed each object to tests that later read it. It checks the patched object graph or retains the potential readers. This covers dependencies that disappear once a class constant has been constructed.

The maps contain observations of the pristine source, tests, fixtures and input queries. In a writable development image, `python /app/backend_sql.py /opt/sqlglot /tmp/backend-sql.bin` and `python /app/assertion_replay.py /opt/sqlglot /tmp/assertion-coverage.bin` regenerate the SQL and assertion indexes. The import-value index can be regenerated with `python /app/derived_values.py /opt/sqlglot /tmp/derived-values.bin`. Use the image's interpreter, hash seed 0 and integration tests enabled. Per-method CPU timings vary between machines.

The comparison archive is for local verification. Submit the contents of the submission archive only.
