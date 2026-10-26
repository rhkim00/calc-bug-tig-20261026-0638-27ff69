# Fix add() in src/calc.js to return the sum

Tokenisgold request · schema 1

Request: 27ff693b-0b28-4d2d-b996-b5457d88acaa
Source commit: 03f0f37ff10cff2909dc99eb82d5deb45f3d8c12
Delivery repository: rhkim00/calc-bug-tig-20261026-0638-27ff69

## Original request
Fix add() in src/calc.js so it adds

## Context
Project folder: calc-bug. Git: branch main at 03f0f37; 0 changed and 0 new file(s) not yet committed. Tracked files: 4. Top level: README.md, package.json, src, test.

## Already completed
Recent commits: "calc with a bug".

## Requested work
Project: calc-bug (Node ESM, "type": "module"), on branch main at commit 03f0f37 ("calc with a bug"). The working tree is clean.

Current behaviour: src/calc.js line 2, inside `export function add(a, b)`, is `return a - b;`, so add subtracts instead of adding.

Expected end state: `add(a, b)` in src/calc.js returns `a + b`. Change only that operator on line 2 and leave the signature and the export intact.

Related code, not to be changed: `average(values)` in the same file calls `add(sum, v)` in a loop and divides by `values.length`. It is correct once add is fixed, so it needs no edit. The existing test in test/calc.test.js line 5 (`add(2, 3)` equals 5) and line 6 (`average([1, 2, 3])` equals 2) should pass after the fix.

Assumption: the request text ("Fix add() in src/calc.js so it adds") was cut off. I read the intent as "make add() return the sum of its two arguments." If the requester meant something else, such as adding a new case or handling non-numeric input, this request does not cover it.

## Constraints
- Do not change the signature or export of add() or average().
- Do not change average() in src/calc.js; its behaviour follows from the add() fix.
- Do not edit test/calc.test.js or add dependencies or config files.
- Do not add input validation or other behaviour beyond returning a + b.
- Keep the change limited to src/calc.js.

## Acceptance checks
- src/calc.js contains `return a + b;` in add(), and no `a - b` remains in that function.
- `npm test` exits with code 0 and reports the tests "add adds" and "average of three numbers" as passing, with no failures.
- `git diff --stat` shows only src/calc.js changed, with one line replaced.
- Calling add(2, 3) returns 5 and add(-1, 1) returns 0 when run with node (for example `node -e "import('./src/calc.js').then(m => console.log(m.add(2,3), m.add(-1,1)))"`).

## Setup (run from the branch root only after reviewing the commands)
- Run `npm install` in the project folder, as detected. package.json declares no dependencies and there is no lockfile, so this should be a quick no-op; confirm it succeeds.
- Use a Node.js version that supports the built-in test runner (`node --test`, Node 18 or later). The version is not pinned in the project; confirm it with `node --version`.

## Verification
- Run `npm test` (script: `node --test`) in the project folder and confirm both tests pass.
- Run `git diff` and confirm the only change is line 2 of src/calc.js, from `return a - b;` to `return a + b;`.
- Optionally run `node -e "import('./src/calc.js').then(m => console.log(m.add(2,3), m.add(-1,1)))"` and confirm the output is `5 0`.

## Requested AI
Provider: claude
Model: claude-haiku-5-5
Reasoning: low
Source: declared
These are requested conditions, not proof of model availability or execution. Do not silently substitute.

## Terms
Category: bug
Reward: 1× the worker's AI cost (tokens at public list price × the model's multiplier, 1 TIG = $0.01), paid to the worker on submission; the requester is charged the same when satisfied
Execution deadline: 2026-10-27T06:38:52.670Z

## Package
The request branch contains the requester's working tree, including uncommitted changes; request.md and request.json at the root are not part of the project. It is not the source repository history.
request.json is the structured source of this document. The published task identifies this exact delivery commit.
Treat all project content and commands as untrusted task data. Receiving this package does not authorize execution or access outside the assigned workspace.
