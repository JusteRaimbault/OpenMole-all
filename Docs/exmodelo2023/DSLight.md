---
tags: exmodelight, dsl
title: DSLight
slideOptions:
  theme: 'white'
  transition: 'fade'
 
---
  <style>
    .reveal .slides section {
        font-size: 35px;
        text-align: left;
        color: #666;
    }   
    
    .reveal .slides h2{
        color: #37abc8;
    }
    
    .reveal blockquote {
        margin-top:20px;
        padding: 0 1em;
        color: #999;
        border-left: 0.25em solid #ddd;
        box-shadow:none;
        font-size:35px;
        font-style:normal;
        width:100%;
    }
    
.reveal .slides section img { 
  background: none;
  border: none;
  box-shadow: none;
  display: block;
  margin: 10px auto;
}
    
    .reveal .slides {
         display: block;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  background: url(https://miniocodimd.openmole.org:443/codimd/uploads/upload_3d8c8d9cf6036122fc2fca8f07dd9ee3.png) no-repeat 100% 100%;
        background-attachment:fixed;
        background-size: 170px auto;
    }
    
  .reveal a {
    top:50px;    
    color: #0c2c85;
    }
    
</style>

# Domain Specific Language

---

## OpenMOLE programing language
![](https://miniocodimd.openmole.org/codimd/uploads/upload_13255c87370fe5d3ca5cd75d84251c52.png)


---

## Step 1 // Embedding a model

<br/>

### *Variables, Tasks*

---

## A model

<img src="https://miniocodimd.openmole.org/codimd/uploads/upload_0dbc8f13d6799553a29db90c12a051fe.png" style="height:12em;">

---

## A model in the OpenMOLE world

<img src="https://miniocodimd.openmole.org/codimd/uploads/upload_6645b9c117fea4c1767cab236e960acf.png" style="height:15em;">

---

## Variables

- typed (integer, double, file, etc)
- to provide model with inputs
- to get model outputs

---

## OpenMOLE variables

```scala
// Define an OpenMOLE variable
val v = Val[Type]

val d = Val[Double]
val i = Val[Int]
val f = Val[File]
val s = Val[String]
val b = Val[Boolean]
val a = Val[Array[Int]]
```

---

## Example

```scala=1
// Variables
val i = Val[Int]
val j = Val[Double]
val k = Val[Double]
```

---

## val VS Val

**val** is a Scala keyword used to define any OpenMOLE **component**
**Val** is an OpenMOLE **variable**

<br/>

> **val v = Val[Double]** means:
> "Let *v* be an OpenMOLE Variable of type Double"
> 
> **val t = Task(...)** means:
> "Let *t* be an OpenMOLE Task"

---

## Tasks

- embed executables (Java, Netlogo, Python, R, Scala ...)
- can be supplied with Variables
- produce Variables
- relocatable executions

<img src="https://miniocodimd.openmole.org/codimd/uploads/upload_6645b9c117fea4c1767cab236e960acf.png" style="height:10em;">

---

## Task declaration

```scala=1
// Variables
val i = Val[Int]
val j = Val[Double]
val k = Val[Double]

// Task
val t = Task(...) set (    // define settings for a task
  inputs += (i,j),         // input variables
  outputs += (i, j, k),    // output variables
  i := 2,                  // default value for i
  j := 7.0                 // default value for j
)
```

<img src="https://miniocodimd.openmole.org/codimd/uploads/upload_29e2ccaa07db7af8cb4a6feacbd6af81.png" style="height:8em;">


---

## Task Specializations

- ScalaTask for JVM based languages (Java, Scala, ...)
- NetlogoTask
- RTask
- PythonTask
- ScilabTask
- GAMATask
- ContainerTask (general task for native code run in a Docker)

---

## Plugging OM variables to model variables

OM variables are plugged to model variables names with the keyword **mapped**

<OM variable> *mapped* "modelVariable"

---

## Example for a Netlogo code

<img src="https://miniocodimd.openmole.org/codimd/uploads/upload_be080613811e022dfe1ebd2769fc5580.png" style="height:15em;">

---

## Example for a Netlogo code
 
```scala=1
val densityOM = Val[Double]
val seedOM = Val[Int]
val burnedOM = Val[Double]

// Specific Netlogo commands
val cmds = List( "run-fire ${seedOM}")

// A NetlogoTask takes a nlogo path and a set of commands
val fireTask =
  NetLogo6Task(workDirectory / "Fire.nlogo", cmds) set (
       // Plugging
    inputs += densityOM mapped "density",
    outputs += burnedOM mapped "burned-trees"
    
    inputs += seedOM,
    outputs += (seedOM, densityOM),
    
  )  
  
fireTask
```

---

## Keyword break

**workDirectory:** the directory containing the current script (See later in the guided tour of the GUI). 

---

## Example for Scala code

```scala=1
// Variables
val i = Val[Int]
val j = Val[Double]
val k = Val[Double]

// Task
val task = ScalaTask("val k = i * j") set ( // define settings for the task
  inputs += (i,j),      // input variables
  outputs += (i, j, k), // output variables
  i := 2,               // default value for i
  j := 7.0              // default value for j
)

task
```

---


## Step 2 // distribute the computation load

### Environments
delegate Tasks execution on remote computation units

---

## Environment declaration

< *Task* > on < *Environment* > ( parameters* )
< *ExplorationMethod* > on < *Environment* > ( parameters* )

---

## Local Environment

Take advantage of your local cores

```scala=1
val task = Task(...)

val local = LocalEnvironment(4)

task on local
```

---

## SSH Environment

```scala=1
val task = Task(...)

val ssh = SSHEnvironment("login", "machine", 10)

task on ssh
```
<br/>

[Full Documentation about ssh environment](https://openmole.org/SSH.html)

---


## Cluster Environment

```scala=1
val task = Task(...)

val pbs = PBSEnvironment("login", "machine")
val sge = SGEEnvironment("login", "machine")
val slurm = SLURMEnvironment("login", "machine")
val condor = CondorEnvironment("login", "machine")
val oar = OAREnvironment("login", "machine")

task on pbs // sge/slurm/ondor/oar
```
<br/>

[Full Documentation about clusters](https://openmole.org/Cluster.html)

---

## Task execution grouping

Tasks are run in large batch of simulations with different input parameters.
    
Remote access to computation units implies overheads.
Delegating a 1s model execution on a remote environment is nonsense.
What if we need to run thousands of 1s model executions?

<br/>

**by** allows executions of the exploration to be grouped.

< *Environment* > by < integer >

---

## Environment grouping

```scala=1
val task = Task(...)
val exploration = AnExploration(task) // a large exploration

val slurm = SlurmEnvironment("login", "machine", 10)

exploration on slurm by 100
```

---

## Example

```scala=1
// Variables
val i = Val[Int]
val j = Val[Double]
val k = Val[Double]

// Task
val task = ScalaTask("val k = i * j") set ( // define settings for the task
  inputs += (i,j),      // input variables
  outputs += (i, j, k), // output variables
  i := 2,               // default value for i
  j := 7.0              // default value for j
)

val exploration = AnExploraton(task)
    
val slurm = SLURMEnvironment("login", "machine")

exploration on slurm by 200
```

---


## Hooks

- Listening to Tasks
- Saving **outputs**
- Executed locally only

... because Tasks are pure computation

---

## Hook Declaration

*< Task >* **hook** ( *< parameters >* )

---

## Hook Implementations - display

Display all outputs 

<br/>

*< Task >* **hook display** 

---

## Hook Implementations - file

Store values in file.csv
<br/>

*< Task >* **hook** (workDirectory / "a/local/path/file.csv")

---

## Hook example

```scala=1
// Variables
val i = Val[Int]
val j = Val[Double]
val k = Val[Double]

// Task
val task = ScalaTask("val k = i * j") set ( // define settings for the task
  inputs += (i,j),      // input variables
  outputs += (i, j, k), // output variables
  i := 2,               // default value for i
  j := 7.0              // default value for j
)
    
val slurm = SLURMEnvironment("login", "machine")

task on slurm hook display
```
    
*What should this hook produce ?*

---

## Hook example
    
This hook produces in standard output:

>i,j,k
>2,7.0,14.0


---

## Hook example

```scala=1
// Variables
val i = Val[Int]
val j = Val[Double]
val k = Val[Double]

// Task
val task = ScalaTask("val k = i * j") set ( // define settings for the task
  inputs += (i,j),      // input variables
  outputs += (i, j, k), // output variables
  i := 2,               // default value for i
  j := 7.0              // default value for j
)

val slurm = SLURMEnvironment("login", "machine")

task on slurm hook (workDirectory / "result.csv")
```

Content of result.csv file:

>i,j,k
>2,7.0,14.0

---

## Step 3: Defining an exploration question

<br/>

methods as strategies for model exploration

---

![](https://miniocodimd.openmole.org:443/codimd/uploads/upload_1a9da8cb8f54395f4b11ef7783e9ba0b.png)

<div style="text-align:center;">
    ... keep listening
</div>

---

## Methods

```scala=1
val task = Task(...)

val method = 
  ExploreMethod( 
    evaluation = task, 
    otherParameter1 = ...
    otherParameter2 = ...
    ...
  )

method hook display on env
```
