# CS2103 Notes
# Week 1

## Overload Constructors
    public Time() {
        this(0, 0, 0);
    }
    public Time(int hour, int minute, int second) {
        this.hour = hour;
        this.minute = minute;
        this.seconds = second;
    }

## Convert double to int using `int`
    x = (int)2.25 // x=2

## Math functions
    Math.PI // Get value of Pi
    Math.pow(x, y) // Raise x to the power of y
    Math.max(x, y)


## Remember getters and setters

## Basic Java program template ***
    public class Main {
        public static void main(String[] args) {
            // ...
            System.out.println(...);
        }
    }

    class Circle {
        // Attributes
        private int hour;
        private int minute;
        private int second;
        
        // Class-level attributes
        private static int numOfCircle = 0;

        // Constructors
        public Circle() {
            this.hour = 0;
            // ...
        }
        // Getters
        public int getHour() {
            return hour;
        }
        // Setters
        public void setHour(int hour) {
            this.hour = hour;
        }
        
    }

    // Inheritance and child class
    class Oval extends Circle {
        public Oval() {
            // Must be in the first line of subclass constructor
            super(); //***
        }
    }

## Enumerations
* Fixed set of values that can be considered as a data type
* Similar to setting levels in a factor in R
* Prevents assignment of invalid values/levels
<!-- To insert code after a list item -->
    public enum Day {
        // Constants, so uppercase
        SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
    }

    Day today = Day.MONDAY;
    Day[] holidays = new Day[]{Day.SATURDAY, Day.SUNDAY};

    switch (today) {
        case SATURDAY:
        case SUNDAY:
            System.out.println("It's the weekend");
            break;
        default:
            System.out.println("It's a week day");
    }

## Type Signature
* Type sequence of the parameters of a method

## Ways to create an array
1.

    Animal[] animals = new Animal[]{
        new Cat("Mittens"),
        new Dog("Spot")
    };
2.

    Shape[] shapes = new Shape[100];

## Abstract Classes
* Class cannot be instantiated, but can be subclasses
* E.g. Animal as generalisation of subclasses Cat, Dog, Horse, Tiger
	* Does not make sense to instantiate Animal object
	* move method of Animal class likely abstract because not impossible to implement a move method at Animal class level to fit all subclasses (all animals move in a different way)
* If a class contains abstract methods, class itself must be abstract
<!-- -->
    public abstract class Animal {
        protected String name;
        public Animal(String name) {
            this.name = name;
        }
        // Note method signature ends with a semicolon, and no method body
        // ***
        public abstract String speak();
    }

* NOTE: Cannot instantiate abstract classes!
* **WRONG**
<!-- -->
    a = new Animal(); // Compile error
* **OKAY**
<!-- -->
    Animal a; // All right to use a type

## Interface
* Behaviour specification, collection of method specifications
* Is a reference type
* Class implementing an interface is an is-a relationship, like class inheritance
<!-- -->
    public interface DrivableVehicle {
        // Can contain constants and static methods
        int MAX_SPEED = 150;

        static boolean isSpeedAllowed(int speed){
            return speed <= MAX_SPEED;
        }

        // Method signatures have no curly braces, terminated with a semicolon
        void turn(Direction direction);
        void changeLanes(Direction direction);
        void signalTurn(Direction direction, boolean signalOn);
    }

    // Cannot be instantiated, only implemented
    public class CarModelX implements DrivableVehicle {
        // ...
    }
    // Can be used a type
    DriveableVehicle dv = new CarModelX();
    // Interface can inherit other (multiple) interfaces 
    public interface SelfDrivableVehicle extends DrivableVehicle {
        void goToAutoPilotMode();
    }

## Substitutability
* Every instance of a subclass is an instance of the superclass, but not vice-versa
* An instance of a subclass can be declared as type of superclass

## Dynamic Binding
* Mechanism where method calls in code are resolved at runtime, rather than at compile time
* E.g. overriden methods

## Static Binding
* Early binding
* When a method call is resolved at compile time
* E.g. overloaded methods, overloaded constructors

## Polymorphism
* 1) Substitutability
	- Able to treat objects of different types as one type
* 2) Overriding
	- Objects of different subclasses can display different behaviours in response to same method call
* 3) Dynamic Binding
	- Polymorphic code can call method of parent class and yet execute implementation of child class

## Collection
* Or "container"
* Object that groups multiple elements into a single unit
* Can store, retrieve, manipulate and communicate aggregate data

* Unified architecture for representing and manipulating collections
* Contains:
	1) Interfaces
		- Abstract data types that represent collections
		- Allow collections to be manipulated independently of the details of their representation
		- e.g. List<E> interface for ArrayList<E>, LinkedList<E>
	2) Implementations
		- Concerete implementations of collection interfaces
		- Reusable data structures
		- e.g. ArrayList<E> implements List<E> interface
		- e.g. HashMap<K, V> implements Map<K, V> interface
	3) Algorithms
		- Methods that perform useful computations on objects that implement collection interfaces
		- Polymorphic, same method can be used on many different implementations of the appropriate collection interface
		- e.g. sort(List<E>) can sort a collection that implements List<E> interface

## Core Collection interfaces
1) Collection: root of collection hierarchy
2) Set: collection that cannot contain duplicate elements
3) List: ordered collection/sequence
4) Queue: collection used to hold multiple elements prior to processing
5) Map: object that maps keys to values

## ArrayList
* Resizable array implementation
<!-- -->
    import java.util.ArrayList;

    ArrayList<String> items = new ArrayList<>();

    items.add("Apple"); // ["Apple"]
    items.contains("Box");
    items.get(2);
    items.size();
    items.clear();

## HashMap
* Collection of key-value pairs
<!-- -->
    import java.awt.Point;
    import java.util.HashMap;
    import java.util.Map;

    HashMap<String, Point> points = new HashMap<>();

    points.put("x1", new Point(0, 0));
    pointAsString(points.get("x1")); //[0,0]
    points.containsKey("x1");
    points.containsValue(new Point(0, 0));

    for (Map.Entry<String, Point> entry : points.entrySet()) {
        print(entry.getKey() + " = " + pointAsString(entry.getValue()));
    }
    
_where pointAsString is a method defined_

## Exception Handling
* HANDLE AND RECOVER FROM PROBLEMS (not PREVENT them)
* When error occurs, application may:
    1) request user intervention
    2) recover on its own
    3) log user off/shut down system (extreme cases)

* Exceptions are used to deal with 'unusual' but not entirely unexpected situations encountered during run time
* 3 basic categories of exceptions in Java
    1) **Checked exceptions**
		- Application anticipates and recovers from
		- Catch exception and notify user of mistake
	- **Unchecked exceptions**
	2) Errors
		- Exceptions external to application
		- Application usually cannot anticipate or recover from
		- Indicated by 'Error' and its subclasses
		- e.g. `java.io.IOError`
		- Program might print stack trace and exit
	3) Runtime exceptions
		- Exceptions internal to application
		- Application usually cannot anticipate or recover from
		- Indicated by '`RuntimeException`' and its subclasses
		- e.g. programming bugs, logic errors, improper use of an API
		- e.g. `NullPointerException`

* How exceptions are typically handled
    - When error occurs some point in execution, code being executed creates an exception object
        - Contains info about error (type, state of program)
    - Hands it off to runtime system, i.e. throwing an exception
    - Runtime system tries to find something to handle in call stack
        - Search for method/code that can handle exception, i.e. exception handler
        - Search begines with method in which error occurred and proceeds through call stack in reverse order in which the methods are called
    - When appropriate handler found, runtime system passes the exception to handler
        - Appropriate handler if type of exception object thrown matches the type that can be handled by the handler
        - i.e. catch the exception

* Advantages of exception handling
	- Ability to propogate error info through the call stack
	- Separation of code that deals with 'unusual' situations from code that does the 'usual' work

* `try`-`catch`-`finally` blocks
	- `try`: identifies block of code in which an exception can occur
	- `catch`: identifies block of code (i.e. exception handler) that can handle a particular type of exception
	- `finally`: specify code that is guaranteed to execute with or without the exception
<!-- -->
    public void writeList() {
        print("starting method");
        try {
            print("starting process");
            process();
            print("finishing process"); // will not be printed if exception occurs in process() - does not execute all of try-block
        // Needs at least one catch/finally-block for try-block
        } catch (IndexOutOfBoundsException e) {
            print("caught IOOBE");

        } catch (IOException e) {
            print("caught IOE");

        } finally {
            // clean up
            print("cleaning up"); // place to close files, recover resources, clean up after code in try-block
        }
        print("finishing method");
    }

* Class of exception object indicates type of exception thrown
* Exception object can contain further info about error, including error message

* `Throw`-statement
<!-- -->
    if (size == 0) {
        throw new EmptyStackException();
    }

* In Java, Checked exceptions have a "Catch or Specify Requirement"
	- Code that might throw checked exceptions must be enclosed in a try-statement (with handler) or method that specifies that it can throw the exception (with throws-clause that lists exception)
<!-- -->
    public void writeList() throws IOException, IndexOutOfBoundsException {
        print("starting method");
        process();
        print("finishing method");
    }

* Examples
    * 
    <!-- -->
        public class IllegalShapeException extends Exception {
        //no other code needed
        } 
    * `NumberFormatException`
    * `IndexOutOfBoundsException`

## Other notes:
* In Java, a class that does not have any abstract methods can be declared as an abstract class
* Subclass should provide implementations for all abstract methods in superclass or else must be also declared abstract
<!-- -->
    shapesCount++; // Increase count in a method
    Integer newValue = Integer.valueOf(roster.get(day).intValue() + 1);

# Week 1 (Lecture - 16/8)

## Main 2 task scenarios in an internship:
1) Greenfield
	- New product
	- Nothing in the field
	- Likely to be a prototype

2) Brownfield
	- Something that is existing
	- Production

## For this module, need:
1) Retention: remember things you learn
2) Fluency: use the concepts in a way a native speaker uses the language

## Git Fork
1. Fork
2. Clone fork
3. Commit changes
4. Push to fork
5. Can pull directly from remote

## Regressions
- Unintended side-effects of fixing a bug
	- e.g. breaking other code
- Automated regression testing of CLI apps
	- Input and expected output files (compare using command '`FC file1 file2`')
	- To detect unintended changes

-----

# CS2103 Notes
# Week 2

## Pros and Cons

### Pros

1. Sheer joy of making things
    - Especially things of his own design
2. Pleasure of making things useful to other people
3. Fascination of fashioning complex puzzle-like objects of interlocking moving parts and watching them work in subtle cycles, playing out the consequences of principles built in from the beginning
4. Joy of always learning
    - Nonrepeating nature of the task
    - Theoretical, practical
5. Delight of working in such a tractable medium
    - Flexible, easy to polish and rework
    - Construct is real, moves and works; visible outputs

### Cons

1. Must perform perfectly
2. Constrained by other's objectives, resources and information
    - Authority, management
3. Dependence upon others
    - Depend on other people's programs
    - Maldesigned, poorly implemented, incompletely delivered (no source code, test cases), poorly documented
    - Spend time studying and fixing things
4. Finding nitty little bugs
    - Tedious, painstaking labour
5. Debugging
    - Last bugs take more time than the first
6. Product appears to be obsolete upon/before completion]
    - Often the last straw

* Implementation of real products demands phasing and quantising
* Obsolescence of an implementation must be measured against other existing implementations, not against unrealised concepts
* Challenge and mission: find real solutions to real problems on actual schedules with available resources

## IDES

* Integrated Development Environments (IDEs) support most development-related work within the same tool
* Generally consists of:
    * Source code editor
        - Includes features: syntax colouring, auto-completion, easy code navigation, error highlighting, code-snippet generation
    * Compiler/and-or interpreter
        - Facilitate compilation, linking, running, deployment of a program
    * Debugger
        - Allows program to be executed one step at a time to observe the run-time behaviour
        - Locate bugs
    * Other tools to aid various aspects of coding
        - Support for automated testing
        - Drag-and-drop construction of UI components (visual programming)
        - Version management support
        - Simulation of target runtime platform
        - Modelling support

### Intellij IDEA
* Import vs opening a project/file
    - Import: uses your own default environment settings
    - Open: uses user's workspace settings

## Automated Testing of Text UIs

### Testing
    1. Operating a system or component under **specified conditions**
    2. **Observing** or recording results
    3. Making an **evaluation** of some aspect of the system or component
* Use inputs and expected output(s), compare with actual output
* Test case
    - Specifies how to perform a test
    - Minimally, specifies input to _software under test_ (SUT) and expected behaviour
    - Based on specification, reviewing similar existing systems, or comparing to the past behaviour of the SUT
    - Can contain:
        - Unique identifier
            - e.g. TC0034-a
        - Descriptive name
            - e.g. verticle scrollbar activation for long web pages
        - Objectives
            - e.g. to check whether the vertical scrollbar is correctly activated when a long web page is loaded to the browser
        - Classification information
            - e.g. priority - medium, category - UI features
        - Cleanup (if any)
            - e.g. empty browser cache
* For each test case: ***
    1. Feed input to SUT
    2. Observe actual output
    3. Compare actual output with expected output
* **Test case failure**
    - Mismatch between expected and actual behaviour
    - Indicates a potential defect/bug (unless error is test case itself)

### Regression Testing

* Regression: unintended, undesirable effects on system
    - caused by modifications in system
* Regression testing: re-testing of software to detect regressions
    - retest all related components, even if they were tested before
    - more effective if done frequently, after each small change
    - more practical if automated

### Test Automation
* Run automated test case programmatically
* Determine result of test case (pass/fail) programmatically
* Pros
    - Reduce effort required to run tests repeatedly
    - Increases precision of testing (less human error)
* Test-driven development (TDD)
    - Tests constantly running on your code in the background
* Write it early from the beginnings of an operation
* Command Line interface (CLI), input/output re-direction:
<!-- -->
    java AddressBook < input.txt > output.txt
    python AddressBook.py < input.txt > output.txt
    FC output.txt expected.txt // file-compare (FC)
    diff output.txt expected.txt

* Only use this technique when:
    1. testing CLI apps
    2. exact output can be predetermined
        - NOT when output varies from one run to another
        - e.g. NOT when contains time stamp


## Revisions History

### Revision Control
* Process of managing multiple versions of a piece of information

### Revision Control Software (RCS)
* Or Version Control Software (VCS)
* Software tools that automate the process of RC
    - Managing revisions of software artifacts
    - Revision: state of a piece of information at a specific time that is a result of some changes to it
        - e.g. modify code, save file -> new revision/version of file
* Track the history and evolution of your project
    - Who made the change, why, when and what
* Makes it easier for you to collaborate
    - Identify and resolve conflicts (multiple people making potentially incompatible changes)
* Helps to recover from mistakes
* Helps you work simultaneously on, and manage the drift between multiple versions of your project

## History

* Stores **history** of working directory as a **series of commits**
    - Commit after each change that is to be remembered
* _committing_
    - saves a snapshot of the current state of the tracked files in version control history/ save the current state of the working folder into the Git revision history
    - each commit is recorded as point in the history of the project, uniquely identified by an auto-generated hash
    - a specific commit can be tagged with a more easily identifiable name
* _stage_
    - Intermediate step allows us to commit only some changes while saving other changes for a later commit
    - prepare a file for committing
* _diff_ 2 commits
    - see what change between 2 points in history
* _checkout_ commit
    - restore state of working directory at a point in the past
* _track and ignore_
    - should ignore temporary log files created during build/test process
* _branches_
    - multiple branches, evolve content in parallel
    - Git creates a default branch `master` on which commits go on by default
* _ignore_
    - `.gitignore` file tells Git which files to ignore when tracking revision history
* _stash_
    - stash uncommitted changes in working directory
    - prevents them from being overwritten when checking out a specific version of history
    - temporarily shelve/stash changes made to working copy


## Repositories
* Repo: **database** of the history of directory that is being tracked by an RCS
    - Stores meta-data about revision history
* Git uses a hidden folder named `.git` inside the working directory where repo initialised

## Git

| Command | Does what | Example | 
| --- | --- | --- |
| `git init` | initialise repo | |
| `ls -a` | view all files (should show `.git` directory) | |
| `git status` | check the status of repo | |
|  `git add` or `git stage` | stage files | `git add fruits.txt` |
| `git commit -m "commit message here"` | commit staged files | |
| `git commit -am "commit message here"` | stage and commit files | |
| `git log` | see commit history | |
| `touch .gitignore` | create `.gitignore` file, edit by vim | |
| `git tag -a tag-name` | add tag to the current commit | `git tag -a v1.0` |
| `git tag` | view tags | |
| `git push origin tag-name` | push a specific tag (remember to push tags to repo, regular `git push` does not do it!) | `git push origin v1.0b` |
| `git push origin --tags` | push all tags | |
| `git show part-of-commit-hash` | show what changed in specific commit |  `git show 251b4cf` |
| `git diff` | show changes (uncommitted) since last commit | |
| `git diff part-of-commit-hash1...part-of-commit-hash2` | shows changes between the points indicated by commit hashes | `git diff 0023cdd..fcd6199` |
| `git diff tag-name..HEAD` | shows changes that happened from the commit tagged by `tag-name` to the most recent commit | `git diff v1.0..HEAD` |
| `git checkout commit-identifier` | change working directory to state it was in at a specific past commit | `git checkout v1.0`, `git checkout 0023cdd`, `git checkout HEAD~2` (state 2 commits behind most recent commit) |
| `git branch -a` | see all branched | |
| `git checkout branch-name` | go back to most recent commit of the current branch | `git checkout master` |
| `git stash` | saves uncommitted changes (both staged and unstaged) away - **won't stash changes made to untracked (new files not yet staged) or ignored files** | |
| `git stash pop` | reapply previously stashed changes to working copy | |
| `git stash apply` | reapply changes to working copy _and_ keep them in stash (useful if want to apply same stashed changes to multiple branches) | |
| `git stash -u` | `git stash` but also stashing untracked files | |
| `git stash -a` or `git stash --all` | `git stash` but also untracked and ignored files | | 
| `git stash list` | view list of multiple stashes made (gives stash identifier) | |
| `git stash save "annotate stash with message"` | annotate stash with description (good when creating multiple stashes) | |
| `git stash pop stash-identifier` | repply specific stash | `git stash pop stash@{2}` |
| `git stash show` | view summary of stash | |
| `git stash show -p` or `git stash show --patch` | view full diff of a stash | |
| `git clone git-repo-URL` | Clone repo to computer | |
| `git reset --hard HEAD~num` | Delete commits at the tip of revision history | `git reset --hard HEAD~2` (deletes last 2 commits) |
| `git pull origin` | Pull latest commits from remote repo | |
| `git push origin master` | Push new commits to remote repo | 

| Changing version history (_use with caution_) | |
| --- | --- |
| `git rebase` | move branch from one location to another |
| `git cherry-pick`| pick only some commits of a branch and then `rebase`-ing it |
| `git squash` | combine multiple commits into a single commit | 

| Pushing an existing local repo | | Example |
| --- | --- | --- |
| | Login to GitHub, create new repo | |
| | Provide name for repo, keep `Initialise this repo ...` tick box unchecked | |
| `https://github.com/{your_user_name}/{repo_name}.git` | Note URL of repo | `https://github.com/johndoe/foobar.git` |
| | Navigate to folder containing remote repo | |
| `git remote add {remote_name} {remote_repo_url}` | Set new remote repo as _remote_ of local repo | `git remote add origin https://github.com/johndoe/foobar.git` |
| `git push -u origin master` | Push to new remote (use `-u` flag to inform Git to track the branch) | |

## Remote Repos
* Copies of a repo hosted on remote computers
    - Can also serve as a remote backup of code base
* _cloning_ a remote repo
    - Create a copy of a remote repo on your computer
    - Includes version history
* _push_ new commits in clone to remote repo
    - Copy new commits onto remote repo
    - Requires write-access
    - If pushing **existing** local repo to new remote repo on GitHub: need to create an empty remote repo on GitHub
        1. On GitHub, create new repo
        2. Provide name for repo, keep `Initialise this repo...` tick box unchecked
        3. Note URL of repo (`https://github.com/{your_user_name}/{repo_name}.git`)
        4. Push
* _pull_ from remote repo
    - Receive new commits in remote repo
    - Sync local repo with latest changes to remote repo
* _fork_
    - Remote copy of a remote repo
    - E.g. When you want to push to a remote repo but do not have write access
    - HowTo: On GitHub, click on the 'Fork' button on the top-right corner of the repo to fork
* _pull request_
    - Mechanism for contributing code to remote repo
    - Formal request sent to maintainers of repo
        - Ask them to pull your new code to their repo
* _track_
    - Remember which branch in the remote repo corresponds to which branch in the local repo

# Duke: Gradle Tutorial
* _Gradle_
    - build automation tool
    - used to automate build processes
* _build file_
    - describes the project
    - mainly consists of:
        1. _plugins_
        2. _tasks_
        3. _properties

| What | | Example |
| --- | --- | --- |
| **Plugins** | Extend the functionality of Gradle | `java` plugin adds support for `Java` projects |
| **Tasks** | Reusable blocks of logic (can be composed of other tasks or be dependent on another task) | Task `clean` simply deletes the project build directory |
| **Properties** | Changes the behaviour of tasks | `mainClassName` of the `application` plugin is a compulsory property which tells Gradle which class is the entrypoint to your application |

# Week 2 Lecture (23/8)

* Don't be complacent.
* Theory (from CS2103) + Experience
    - Making connections between the 2
* Multi-cursor

## Intellij

| Command | Description |
| --- | --- |
| `CTRL-Q` | See Quick Documentation |
| `CTRL-Click` | See source code of method |
| `CTRL-D` | Duplicates selected block or current line (if no block selected) |
| `Shift-Tab`| Unindent line |
| `CTRL-Shift-A` | Help/Search |

## Good Code

* Code quality is important
* Readability
* Practices for better code
    1. Standardise
        - Should look like a single person typed it, no matter how many contributors
        - Capitalisation
        - Indentation
        - etc.
    2. ...

## Finding bugs
- QA Tester
    - Can only happen at the end
    - More costly, more to change and fix
    - Mistakes would be publicised and recorded, uploaded on the bug tracker for you to fix eventually
- Developers
    - Find sooner, the better

## Automated Testing
* Testing frameworks
    - JUnit
    - Need both drivers and stubs
* JUnit
    - Annotate with `@` to show that it is a test
    - Use `assetEquals` in method used for testing
        - e.g. `testExecuteUserCommand`
        - Each line starting with this is another test
    - 3rd party library, needs to be imported
    - Run with the green triangle symbol

## Branches
- Useful when you want to try a new approach
    - You don't have to delete the current working code
- `HEAD` indicates which version of files you are currently checking out
- Fast-forward merge
    1. When you have a branch, made some commits there
    2. No changes in `Master`
    3. Just directly merge (kinda like shifting commits over to `Master`branch)
- Good practice to merge without fast-forward
    - Just to log and see the merge
    - Use flag (`git merge --no-ff`)
- When branch off too early, when new commits made to `Master` is wanted in the branch as well
    - Merge `Master`to branch
    - Or user `rebase`
        - As if branch was done later
        - A bit dangerous, be careful, rewriting history
        - Need to force-push to remote
        - A mess if other people have copied the old history
        - Generally, not rewrite history in collaboration projects
- Create a new branch from `Master`
    - Branches can have branches

## Pull Request
* CS2103
    - [Name] Duke Increments

## iP
* Make it your own
    - Give bot any name/personality
    - Don't change repo name
* Opportunity to level-up and/or showcase skills
* Bots will only do superficial process check
    - Subject to human reviewers later
* Assume future to be unknown
    - Implement each increment to the best you can but without considering future increments